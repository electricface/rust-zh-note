

解析命令行选项 
-h 与 --help 选项
-o 带参数

```rust
extern mod extra;
use extra::getopts::{optopt,optflag,getopts};
use std::os;

fn print_usage(program: &str ) {
	println!("Usage: {} [options]
	-o\t\tOutput
	-h --help\tUsage", program);
}

fn main(){
	let args = os::args();
	let program = args[0].clone();
	let opts = ~[ 
		optopt("o"),
		optflag("h"),
		optflag("help"),
	];

	let matches = match getopts(args.tail(), opts) {
		Ok(m) => {m},
		Err(f) => { fail!(f.to_err_msg() ) }
	};

	if matches.opt_present("h") || matches.opt_present("help"){
		print_usage( program );
		return;
	}

	match matches.opt_str("o"){
		Some(output) => {
			println!("get output argument: {}" , output );
			},
		None => {
			print_usage( program );
			return;
		}
	}
}

```
