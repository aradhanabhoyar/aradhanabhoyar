fn reverse_alternate(initial: &str) ->
String {
  let chars: Vec<char> =
initial.chars().collect();
  let mut reversed = String::new();
let mut index = initial.len()-1;
loop{
  reversed.push(chars [index]);
  if index == 0 {
  break;
  }
  index= -1;
  }
  reversed
}
fn main() {
let reversed =
reverse_alternate("cat");
println!("{reversed}");
}
