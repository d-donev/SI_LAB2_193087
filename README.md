# Втора лабораториска вежба по Софтверско инженерство
## Димитарчо Донев, бр. на индекс 193087
  
## Control Flow Graph  
  ![image](https://user-images.githubusercontent.com/80148999/119221252-c1b85d00-baee-11eb-995e-486c5efe8952.png)  
    
## Цикломатска комплексност  
Цикломатската комплексност на графот е 8. Се добива со помош на формулата P+1, каде што P е бројот на предикатни јазли.  
  
## Тест случаи според критериумот Every branch  
  
30-31  
31-31.1  
31.1-32  
31.1-50  
32-33  
33-34  
33-38  
34-35  
34-36  
36-37  
38-39  
39-40  
39-41  
41-42  
42-44  
42-43  
43-31.2  
44-45  
38-46  
46-47  
47-31.2  
46-48  
48-49  
  
  
   @Test  
      void everyBranch() {  
        
RuntimeException temp;  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(-3,35,55))));  
assertTrue(temp.getMessage().contains("The hours are smaller than the minimum"));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(23, 68, 49))));  
assertTrue(temp.getMessage().contains("The minutes are not valid!"));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(30, 29, 49))));  
assertTrue(temp.getMessage().contains("The hours are grater than the maximum"));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(24, 21, 31))));  
assertTrue(temp.getMessage().contains("The time is greater than the maximum"));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(22, 40, 80))));  
assertTrue(temp.getMessage().contains("The seconds are not valid"));  
  
assertEquals(returnList(73552), SILab2.function(createList(new Time(20,25,52))));  
  
assertEquals(returnList(86400), SILab2.function(createList(new Time(24,0,0))));  
  
List<Time> emptyList = new ArrayList<Time>(0);  
assertEquals(emptyList, SILab2.function(emptyList));  
    }  
  
  ## Тест случаи според критериумот Multiple Condition  
    @Test
    void multipleCondition() { 
  RuntimeException temp;  
  
//if (hr < 0 || hr > 24) { //33  
//T X  
//F T  
//F F  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(-10,30,50))));  
assertTrue(temp.getMessage().contains("The hours are smaller than the minimum"));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(30,30,50))));  
assertTrue(temp.getMessage().contains("The hours are grater than the maximum"));  
  
assertEquals(returnList(73550), SILab2.function(createList(new Time(20,25,50))));  
  
//if (min < 0 || min > 59) //39  
//T X  
//F T  
//F F  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(10,-20,50))));  
assertTrue(temp.getMessage().contains("The minutes are not valid"));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(14,75,50))));  
assertTrue(temp.getMessage().contains("The minutes are not valid"));  
  
assertEquals(returnList(73550), SILab2.function(createList(new Time(20,25,50))));  
  
//if (sec >= 0 && sec <= 59) //42  
//T T  
//T F  
//F X  
  
assertEquals(returnList(73550), SILab2.function(createList(new Time(20,25,50))));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(14,40,70))));  
assertTrue(temp.getMessage().contains("The seconds are not valid"));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(14,40,-30))));  
assertTrue(temp.getMessage().contains("The seconds are not valid"));  
  
//else if (hr == 24 && min == 0 && sec == 0) { //46  
//T T T  
//T T F  
//T F X  
//F X X  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(24,0,10))));  
assertTrue(temp.getMessage().contains("The time is greater than the maximum"));  
  
temp = assertThrows(RuntimeException.class, () -> SILab2.function(createList(new Time(24,15,16))));  
assertTrue(temp.getMessage().contains("The time is greater than the maximum"));  
  
assertEquals(returnList(73550), SILab2.function(createList(new Time(20,25,50))));  
   
    }
  
  
   ## Објаснување на напишаните unit tests  
  Unit тестовите се пишувани на начин да се исполнат сите услови и да можат да се поминат сите exceptions. Со употреба на  assertThrows се фаќаат exceptions кои се праќаат во „temp“, a за да може да се провери дали се фрлил соодветниот exception се користи  assertTrue за дадениот влез. Исто така се употребува и  assertEquals за да се провери дали  програмата го враќа точниот резултат за дадениот инпут.  
    
  Со multiple condition се проверуваат сите if услови каде што има повеќе од еден услов. Исто така и овде се користи assertThrows и assertTrue за фаќање и проверување дали е точен даден exception и assertEquals за проверување дали програмата враќа точен резултат за даден влез.  
  
  
