Operations take input and produce an output.

- Append 0/1 appends 0/1 to binary number
	- 1b app0 = 10b (1d -> 3d)
	- 101b app1 = 1011b (5d-> 11d)

Each Operation is a [[Node]] with some number of ins and outs, noted (ins, outs). Eg. initial node providing 0 will be (0, N) meaning 0 ins and N (variable) outs, Duplicator node will have (1, N <= 2)

Each Operation has a [[Cost]], set arbitrarily by me to encourage more creative solutions. Will have to be balanced via playing, but things like replicator and duplicator should have high cost due to being easy to use and things like xor should have low cost due to needing more thought to use. 

Current [[List of Operations]]