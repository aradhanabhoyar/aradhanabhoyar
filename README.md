fn is_palindrome(s: &str) -> bool {
    let s_lower = s.to_lowercase();
 s_lower.chars().eq(s_lower.chars().rev())
}
fn main() {
    let string1 = "madam"; 
    let string2 = "hello"; 
    if is_palindrome(string1) {
        println!("'{}' is a palindrome.", string1);
    } else {
        println!("'{}' is not a palindrome.", string1);
    }
if is_palindrome(string2) {
        println!("'{}' is a palindrome.", string2);
    } else {
        println!("'{}' is not a palindrome.", string2);
    }
}
