# sheet3

    public static int[] Down(String[] v,int n, int i,int j,String x,int[] b){
        if(v[i].charAt(j)!=x.charAt(0)||i>=v.length){
            return b;
        }else{
            b[0]=n;
            b[1]=i-1;
            b[2]=j;
            n++;
            if(j-1>0){
                Left(v,n,i+1,j,x,b);
            }
            if(j+1<v[i].length()){
                Right(v,n,i+1,j,x,b);
            }
            return Down(v,n,i+1,j,x,b)
        }
    }

    public static int[] Right(String[] v,int n, int i,int j,String x,int[] b){
        if(j==v[i].length()||v[i].charAt(j)!=x.charAt(0)){
            return b;
        }else{
            b[0]=n;
            b[1]=i;
            b[2]=j-1;
            n++;
            if(i+1<v.length){
                Down(v,n,i,j+1,x,b);
            }
            if(i-1>0){
                UP(v,n,i,j+1,x,b);
            }
        }
        return Right(v,n,i,j+1,x,b);
    }

    public static int[] Left(String[] v,int n, int i,int j,String x,int[] b){
        if(j<0||v[i].charAt(j)!=x.charAt(0)||j==0){
            return b;
        }else {
            b[0]=n;
            b[1]=i
            b[2]=j+1;
            n++;
            if(i+1<v.length){
                Down(v,n,i,j-1,x,b);
            }
            if(i-1>0){
                UP(v,n,i,j-1,x,b);
            }
            return Left(v,n,i,j-1,x,b);
        }
    }

    public static int[] UP(String[] v,int n, int i,int j,String x,int[] b){
        if(i<0||v[i].charAt(j)!=x.charAt(0)){
            return b;
        }else{
            b[0]=n;
            b[1]=i+1;
            b[2]=j;
            n++;
            if(j+1<v[i].length()){
                Right(v,n,i-1,j,x,b);
            }
            if(j-1>0){
                Left(v,n,i-1,j,x,b);
            }
            return UP(v,n,i-1,j,x,b);
        }
    }

    public static void findplayer(String[] photo,int team,int threshold){
        int n=0;
        int[] arr1=new int[3];
        int[] arr2=new int[3];
        int[] arr3=new int[3];
        int[] arr4=new int[3];
        int[][] square=new int[50][2];
        String v=Integer.toString(team);
        int k=0,i,j,area,y;
        for(i=0;i<photo.length;i++){
            for(j=0;j<photo[i].length();j++){
                arr1=Down(photo,n,i,j,v,arr1);
                arr2=UP(photo,n,i,j,v,arr2);
                arr3=Left(photo,n,i,j,v,arr3);
                arr4=Right(photo,n,i,j,v,arr4);
                n=arr1[0]+arr2[0]+arr3[0]+arr4[0];
                area=n*4;
                if(area==threshold||area>threshold){
                    for(y=0;y<3;y++){
                        System.out.println(arr2[y]);
                    }
                    square[k][0]=(arr1[1]+arr2[1]+1)/2;
                    square[k][1]=(arr3[2]+arr4[2]+1)/2;
                    k++;
                }
            }
        }
        for(i=0;i<50;i++){
            for(j=0;j<2;j++){
                System.out.printf("%d",square[i][j]);
            }
            System.out.println();
        }
    }
}
