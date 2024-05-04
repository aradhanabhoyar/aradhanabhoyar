fn longest_con_seq(s1:&String, s2:&String) -> String {
     let mut max: Option<String> = None;
    let mut current = String::new(); 
    let mut s1_iter = s1.chars().peekable(); 
    let mut s2_iter = s2.chars(); 
    let mut s2_prev_pos = s2_iter.clone(); 
    let mut s1_prev_pos = s1_iter.clone(); 

    loop {  
        let s1_char = s1_iter.next(); 
        if current.len() == 0
        {
            s1_prev_pos = s1_iter.clone()
        }
        match s1_char{
            Some(s1_char)=>
            {   
                loop{    
                    match s2_iter.next()
                    {
                        Some(s2_char) if s1_char == s2_char => {
                            current.push(s1_char);
                            s2_prev_pos = s2_iter.clone();
                            break;
                        },
                        Some(_)=>continue,
                        None=>{
                            s2_iter = s2_prev_pos.clone();
                            break;
                        },
                    }
                }
            },
            None=>{
                match s1_prev_pos.peek()
                {
                    Some(_) => {
                        match max{
                            Some(_) => {
                                let max_str = max.clone();
                                let max_str = max_str.unwrap();
                                if max_str.len() < current.len(){
                                    max = Some(current.clone());
                                }
                                current.clear();
                            },
                            None => {
                                max = Some(current.clone());
                                current.clear();
                            },
                        }
                        s1_iter = s1_prev_pos.clone();
                        s2_iter = s2.chars();
                    },
                    None => break,
                }
            },
        }
    }
    if let Some(_) = max {
        return max.unwrap();
    } else {
        return String::from("");
    }
}
fn criterion_benchmark(c: &mut Criterion) {
    let s1 = "GXTKAYB".to_owned();
    let s2 = "AGGTAB".to_owned();
    c.bench_function("Benchmark", move |b| b.iter(|| longest_con_seq(&s1, &s2)));
}
criterion_group!(benches, criterion_benchmark);
criterion_main!(benches);
