fn is_prime(num: u64) -> bool {
    if num <= 1 {
        return false; 
    }
    for i in 2..=(num as f64).sqrt() as u64 {
        if num % i == 0 {
            return false; 
        }
    }
     true 
}
fn main() {
    let num = 17; 
    
    if is_prime(num) {
        println!("{} is prime", num);
    } else {
        println!("{} is not prime", num);
    }
}
