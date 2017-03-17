Word Ladder II

方法一：

BFS

time \(26\*l\)^h

space \(26\*l\)^h

```java
public static List<List<String>> findLaddersBFS(String beginWord, String endWord, List<String> wordList) {
        List<List<String>> ret=new ArrayList<>();
        if(beginWord==null&&beginWord.length()==0||endWord==null||endWord.length()==0||beginWord.length()!=endWord.length()||wordList.length()==0)
            return ret;
        HashSet<String> dict=new HashSet<>();
        for(String s: wordList)
            dict.add(s);
        List<String> temp=new ArrayList<>();
        temp.add(beginWord);
        ret.add(temp);
        boolean isFound=false;
        
        while(!isFound&&ret.size()!=0){
        //while(!isFound){
            List<List<String>> next=new ArrayList<>();
            for(List<String> list:ret){
                String origin=list.get(list.size()-1);
                for(int i=0;i<origin.length();i++){
                    for(char c='a';c<='z';c++){
                        if(c!=origin.charAt(i)){
                            String transform=replace(origin, i, c);
                            if(dict.contains(transform)){
                                ArrayList<String> newList=new ArrayList<String>(list);
                                newList.add(transform);
                                next.add(newList);
                                
                                //
                                if(transform.equals(endWord))
                                    isFound=true;
                            }
                        }
                    }
                }
            }

            //at the end of each level ,remember to remove the word from the list, else it will has loop
            for(List<String> s:next){
                dict.remove(s.get(s.size()-1));
            }
           
            ret=next;
            next=new ArrayList<>();
        }
        return ret;
    }

public String replace(String s, int k, char c){

}
```

注意：1.每一层的位置，要把刚新加的词从dict中remove掉，不然会出现 abc-&gt;abd-&gt;abc这样的循环不合法



方法二：

双向BFS

time \(26\*l\)^\(h/2\)

space \(26\*l\)^\(h/2\) 

```java
public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        List<List<String>> ret=new ArrayList<>();
        if(beginWord==null&&beginWord.length()==0||endWord==null||endWord.length()==0||beginWord.length()!=endWord.length()||wordList.length()==0)
            return ret;
        HashSet<String> dict=new HashSet<>();
        for(String s: wordList)
            dict.add(s);
            
        HashMap<String,List<List<String>>> from=new HashSet<>;
        HashMap<String,List<List<String>>> to=new HashSet<>;
        
        List<List<String>> tempStart=new ArrayList<>()
        List<List<String>> tempEnd=new ArrayList<>()
        
        from.put(beginWord,tempStart);
        to.put(endWord,tempEnd);
          
        boolean isFound=false;
        while(from.size()!=0&&to.size()!=0!&&isFound){
            HashSet<String,List<List<String>>> next=new ArrayList<String>();
            
            for(String origin: from.keySet()){
                for(int i=0;i<origin.length();i++){
                    for(char c='a';c<='z';c++){
                        if(c!=origin.get(i)){
                            String newStr=replace(origin, i, c);
                            
                            //
                            if(to.keySet().contains(newStr)){
                                isFound==true;
                                //adding to result; merge two list to ret
                                List<List<String> fromList=from.get(origin);
                                
                                for(List<String> l:to.get(newStr)){
                                    List<String> endList=new arrayList<>(l);
                                    Collections.reverse(endList)；
                                    for(List<String> k:fromList){
                                      List<String> tempres=new ArrayList<>(endList);
                                      tempPres.addAll(endList);
                                      ret.add(tempPres);
                                    }
                                }  
                            }
                            //do not found in to hashmap, build next level
                            else if(dict.contains(newStr)){
                                //build the new list for current newstr
                                List<List<String>> list =new arrayList<>();
                                for(List<String> l: from.get(origin))
                                    list.add(new ArrayList<String>(l))
                                
                                for(List<String>l:list)
                                    l.add(newStr);
                                
                                //put it in next 
                                List<List<String> temp=next.get(newStr);
                                if(temp==null)
                                next.put(newStr,list);
                                else
                                { temp.addAll(list);
                                  next.put(newStr,list);
                                }
                            }
                        }
                    }
                }
            }
            
            for(String s:next.keySet())
            dict.remove(s);
            
            if(next.size()<=end.size())
            star=next；
            else
            { start=end;
            end=next;
            
            ｝        
            
        
        }
        //reverse the rt, if the first letter of rt is not equals to beginWord
        for (List<String> l : rt) {
            if (!l.get(0).equals(beginWord)) {
                Collections.reverse(l);
            }
        }
}
```





