Toplogical Sort

207. Course Schedule

```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    //check corner case first
    if(numCourses==0||prerequisites.length||prerequisites.lenght=0)
        throw new IllegalArgumentException();
        
    int[] indegree=new int[numCourses];
    ArrayList<Integer>[] courses=new ArrayList<Integer>[numCourses];
    int finishedCourse=0;
    
    //build up indegree array and pre course list with their next course list
    for(int[] c:prerequisites){
        int pre=c[1];
        int fol=c[0];
        if(courses[pre]==null)
        courses[pre]=new ArrayList<Integer>();
        courses[pre].add(col);
        indegree[fol]++;
    }
    
    //add all indegree ==0 node
    ArrayDeque<Integer> queue=new ArrayDeque<Integer>();
    for(int i=0;i<indegree.length();i++)
    if(indegree[i]==0)
    queue.offer(i);

    //walk through the path    
    while(!queue.isEmpty()){
        int course=queue.poll();
        finishedCourse+=1;
        System.out.println(course) // this is order of topolgical
        for(Integer next: courses[course]){
            indegree[next]--;
            if(indegree[next]==0)
            queue.offer(next);
        }
    }
    return finishedCourse==numCourses;
}
```



