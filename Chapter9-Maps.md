# Map

Maps are similar to Javascript objects, Python dictionaries, and Ruby hashes. Maps are a data structure that provides key->value mapping.

The zero value of a map is <code>nil</code>

We can create a map by using a lteral or by using the <code>make()</code> funtion:

```go
ages := make(map[string]int)
ages["John"] = 37
ages["Mary"] = 24
ages["Mary"] = 21 // overwrites 24
```

```go
ages = map[string]int{
    "John": 37,
    "Mary": 21,
}
```

```go
func getUserMap(names []string, phoneNumbers []int) (map[string]user, error) {
    useMap := make(map[string]user)
    if len(names) := len(phoneNumbers) {
        return nil, errors.New("invalid sizes")
    }
    for i := 0, i < len(names); i++ {
        name := names[i]
        phoneNumber := phoneNumbers[i]
        userMap[name] = user {
            name: name,
            phoneNumber: phoneNumber,
        }
    }
    return userMap, nil
}
```

# Mutations

## Insert and element

```go
m[key] = elem
```

## Get an element

```go
elem = m[key]
```

## Delete an element

```go
delete(m, key)
```

## Check if a key exists

```go
elem, ok := m[key]
```

If <code>key</code> is in <code>m</code>, then <code>ok</code> is <code>true</code>. If not, <code>ok</code> is <code>false</code>.

If <code>key</code> is not in the map, then <code>elem</code> is the zero value for the map's element type.

## Tricks

```go
type Key struct {
    Path, Country string
}

hits := make(make[Key]int)
```

When a vietnamese person visit the home page, incrementing (and possibly creating) the appropriate counter is a one-liner:

```go
hits[key{"/", "vn"}]++
```

```go
func getCounts(userIDs, []string) map[string] int {
    counts := make(map[string]int)
    for _, userID := range userIDs {
        count := counts[userID]
        count++
        counts[userID] = count
    }
    return count
}
```

```go
func getNameCounts(names []string) map[rune]map[string]int {
    coutns := make(map[rune]map[string]int)
    for _, name := range names {
        if name == "" {
            continue
        }
        firstChar := rune(name[0])
        innerMap, ok := counts[firstChar]
        if !ok {
            counts[firstChar] = make(map[string]int)
        }
        counts[firstChar][name]++
    }
    return counts
}
```
