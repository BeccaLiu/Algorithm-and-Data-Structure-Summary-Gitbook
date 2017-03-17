Implement a Trie

```java
class Trie{
TrieNode root;

public Trie(){
root=new TrieNode();
}

public void insert(String word){
    TrieNode curr=root;
    for(char c:word.toCharArray()){
        if(curr.nodes[c-'a']==null){
            curr.nodes[c-'a']=new TrieNode();
        }
        curr=curr.nodes[index];
    }
    curr.isWord=true;
}

public void search(String word){
    TrieNode curr=root;
    for(char c:word.toCharArray()){
        if(curr.nodes[c-'a']==null)
        return false;
        curr=cuur.nodes[index];
    }
    return curr.isWord;
}

private class TrieNode{
    TrieNode[] nodes;
    Boolean isWord;
    
    public TrieNode(){
    isWord=false;
    nodes=new TrieNode[26];
    }
}

}
```



