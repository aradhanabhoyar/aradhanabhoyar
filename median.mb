fn main() {
    let mut integers = vec![
        4, 9, 6, 7, 3, 4, 5, 6, 2, 13, 9, 5, 2, 3, 6, 8, 4, 5, 5, 6, 9, 8, 6,
    ];
    integers.sort_by(|a, b| a.cmp(b));
    let int_length = integers.len();
    if let 0 = int_length % 2 {
        let mut answer = 0;
        answer = int_length / 2;
        let median = (integers[answer] + integers[answer + 1]) / 2;
        println!("the median is {}", median)
    } else {
        let mut answer = 0;
        answer = int_length / 2 + 0.5 as usize;
        let median = integers[answer];
        println!("the median is {}", median)
    }
    let mut values_in_hashmap = HashMap::new();
    for values in integers {
        let count = values_in_hashmap.entry(values).or_insert(0);
        *count += 1;
    }
 let mut current_highest_value = 0;
    let mut modes = vec![];
    for (key, value) in &values_in_hashmap {
        if value > &current_highest_value {
            current_highest_value = *value;
        }
    }
    for (key, value) in &values_in_hashmap {
        if *value == current_highest_value {
            modes.push(key)
        }
    }
    println!(" the modes {:?}", modes);
}
