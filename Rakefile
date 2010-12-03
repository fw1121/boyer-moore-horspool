verbose false

file 'test' => 'test.cpp' do
	sh "g++ -Wall test.cpp -o test -O2"
end

def benchmark(haystack_title, haystack_file, needle = "I have control\n", iterations = 10)
	puts
	puts "# Matching #{needle.inspect} in \"#{haystack_title}\", #{iterations} iterations"
	sh './test', haystack_file, needle, iterations.to_s
end

task :benchmark => 'test' do
	puts "######### Good needle #########"
	benchmark('Random binary data', 'binary.dat')
	benchmark('Only newlines', 'newlines.txt')
	benchmark('Alice in Wonderland (200 MB)', 'alice.html')
	benchmark('Alice in Wonderland (8 KB)', 'alice-small.html', "I have control\n", 500_000)
	
	puts
	puts "######### Bad needle, likely to hit worst-case performance #########"
	needle = "I have control\n\n"
	benchmark('Random binary data', 'binary.dat', needle)
	benchmark('Only newlines', 'newlines.txt', needle)
	benchmark('Alice in Wonderland (200 MB)', 'alice.html', needle)
	benchmark('Alice in Wonderland (8 KB)', 'alice-small.html', needle, 500_000)
end