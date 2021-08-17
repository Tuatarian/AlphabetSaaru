Each node has a [[NodeType | type]] (the Node's [[Operations  | Operation]])

The nodes will be a custom type, tentatively

	type OpNode
		pos : Vector2
		inps : seq[string]]
		out : [string]
		op : nodeType
		connections : seq[int]

Nodetype being a way to internally represent what Operation a node is to perform