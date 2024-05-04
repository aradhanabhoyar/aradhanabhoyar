struct Solution;
impl Solution 
{
    fn search(nums: Vec<i32>, target: i32) -> i32 {
        for i in 0..nums.len(){
            if nums[i] == target.try_into().unwrap() 
			{
				return i.try_into().unwrap()
			}
        }
		-1
    }
}

fn main() {
    let nums = vec![-1, 0, 3, 5, 9, 12];
    let target = 9;
    let my_search = Solution::search(nums, target);
	println!("{}", my_search)
}
