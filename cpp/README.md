# lambda-options

A modern command-line parser for C++.

* Easy to use. The API is expressive.
* Easy to learn. The API is tiny and simple.
* Easy to integrate. Contained in a single [header file](src/LambdaOptions.h?ts=4).
* BSD 1-Clause License

This library is designed to be an intuitive alternative to other C++ command-line libraries such as: Boost.Program_Options, GNU Getopt, TCLAP, and others.

Quick installation: Download the required header here: [src/LambdaOptions.h](src/LambdaOptions.h?ts=4)

* Examples: [example](example)
* Documentation: [API-Index](https://github.com/thomaseding/wiki-lambda-options-cpp/wiki/API-Index)

--------------

Basic example:
```cpp
#include "LambdaOptions.h"
#include <iostream>

int main (int argc, char ** argv)
{
	using namespace lambda_options::with_char;

	Options opts;

	opts.AddOption(Keyword("help", "h"), [] () {
		std::cout << "--user NAME [AGE]" << std::endl;
	});
	opts.AddOption("user", [] (std::string name) {
		std::cout << "Name:" << name << std::endl;
	});
	opts.AddOption("user", [] (std::string name, unsigned int age) {
		std::cout << "Name:" << name << " Age:" << age << std::endl;
	});

	auto parseContext = opts.CreateParseContext(argv + 1, argv + argc);

	try {
		parseContext.Run();
	}
	catch (ParseFailedException const &) {
		return 1;
	}

	return 0;
}
```

