#### 抽奖概率算法 
```java

//mulriple =10000
    public static void main(String[] args) {
        int lastScope = 0;
        Map<Integer, int[]> awardItemScope = new HashMap<Integer, int[]>();
        for (int i = 0; i < 4; i++) {

            int currentScope = lastScope + new BigDecimal((i+1) * 0.1).multiply(new BigDecimal(mulriple)).intValue();
            awardItemScope.put(i, new int[]{lastScope + 1, currentScope});
            lastScope = currentScope;
        }

        int luckyNumber = new Random().nextInt(mulriple)+1;
        int luckyPrizeId = 0;

        Set<Map.Entry<Integer, int[]>> set = awardItemScope.entrySet();
        System.out.println("luckyNumber:"+luckyNumber);
        for (Map.Entry<Integer, int[]> entry : set) {
            System.out.println(entry.getValue()[0] + "=" + entry.getValue()[1]);
            if (luckyNumber >= entry.getValue()[0] && luckyNumber <= entry.getValue()[1]) {
                luckyPrizeId = entry.getKey();
                System.out.println("luckyPrizeId:"+luckyPrizeId);
                break;
            }
        }
    }
```

解析 ： 
画一块10000份的转盘，根据奖品的概率 算出每一个占用多少份 ，然后按照顺排在一起 

空白的部分为不中奖
 然后扔出一个10000个点数的筛子 ，在哪个数值上则表示是哪个奖品


 