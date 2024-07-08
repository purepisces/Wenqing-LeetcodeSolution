In number of islands, when we make visit = set()
and  visit.add((r,c))
we should not visit.add([r,c]) since type 'list' is unhashable
