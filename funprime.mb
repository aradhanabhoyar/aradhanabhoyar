fn check_prime(n:usize) -> bool{
let mut i = 2;
    while i*i<=n {
        if n%i == 0 {
            return false;
        }
        i+=1;
    }
    return true;
}
pub fn main() {
    let n = take_int();
 if check_prime(n) {
        println!("Yes, given number is a prime number");
    }
    else {
        println!("No, given number is not a prime number");
    }
}
