## Load the training data and normalize

```playground
require "csv"
require "shainet"

# use binary dummy columns for `Outcome` column
label = {
  "0" => [1.to_f64, 0.to_f64],
  "1" => [0.to_f64, 1.to_f64],
}

# data structures to hold the input and results
inputs = Array(Array(Float64)).new
outputs = Array(Array(Float64)).new

# read the file
raw = File.read("./data/heart-disease.csv")
csv = CSV.new(raw, headers: true)

# we don't want these columns so we won't load them
headers = csv.headers.reject { |h| ["slope", "ca", "thal", "num"].includes?(h) }

# load the data structures
while (csv.next)
  missing_data = false
  row_arr = Array(Float64).new
  headers.each do |header|
    if csv.row[header] == "?"
      missing_data = true
    else
      row_arr << csv.row[header].to_f64
    end
  end
  inputs << row_arr unless missing_data
  outputs << label[csv.row["num"]]
end

# normalize the data
normalized = SHAInet::TrainingData.new(inputs, outputs)
normalized.normalize_min_max
```

## Create the model, train and save

```playground
# create a network
model : SHAInet::Network = SHAInet::Network.new
model.add_layer(:input, 10, :memory)
model.add_layer(:hidden, 10, :memory)
model.add_layer(:output, 2, :memory)
model.fully_connect

# params for sgdm
model.learning_rate = 0.01
model.momentum = 0.01

# train the network
model.train(normalized.data.shuffle, :sgdm, :mse, epoch = 1000, threshold = -1.0, log = 100)

# save to file
model.save_to_file("./model/heart-disease.nn")
```

## Determine Accuracy

```playground
tn = tp = fn = fp = 0

# determine accuracy
normalized.normalized_inputs.each_with_index do |test, idx|
  results = model.run(test)
  if results[0] < 0.5
    if outputs[idx][0] == 0.0
      tn += 1
    else
      fn += 1
    end
  else
    if outputs[idx][0] == 0.0
      fp += 1
    else
      tp += 1
    end
  end
end

puts "Training size: #{outputs.size}"
puts "----------------------"
puts "TN: #{tn} | FP: #{fp}"
puts "----------------------"
puts "FN: #{fn} | TP: #{tp}"
puts "----------------------"
puts "Accuracy: #{(tn + tp) / outputs.size.to_f}"
## Load and Run the Model
```

## Try it out

```playground
require "shainet"

model : SHAInet::Network = SHAInet::Network.new
model.load_from_file("./model/heart-disease.nn")

# age, sex, chest pain type, bp, chol, sugar > 120, ecg, max heart rate, induced angina, induced ST depression
results = model.run([49, 1, 4, 140, 172, 0, 0.22, 181, 0, 0])
puts "There is a #{((1 - results[0]) * 100).round} percent chance you have heart disease"
```
