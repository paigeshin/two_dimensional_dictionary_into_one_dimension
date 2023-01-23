# two_dimensional_dictionary_into_one_dimension

``swift

fileprivate extension Dictionary {
    var flattened: [String: Any] {
        func flattenRec(output: inout [String: Any], keyPath: String, value: Any) {
            if value is String {
                output[keyPath] = value
            }
            if let dict = value as? [String: Any] {
                dict.forEach { key, value in
                    flattenRec(output: &output, keyPath: "\(keyPath).\(key)", value: value)
                }
            }
        }
        
        var outputDict = [String: Any]()
        
        self.forEach { key, value in
            flattenRec(output: &outputDict, keyPath: key as! String, value: value)
        }
        
        return outputDict
    }
}


```
