# Lafore-3-BublSort

import java.util.Date;

class Algorithm {

    static class OrdArray {
        private long[] a;
        private int nElems;

        public OrdArray(int size){
            a = new long[size];
            nElems = 0;
        }

        public int getSize(){
            return nElems;
        }

        public void display(){
            for (int j = 0; j < nElems; j++)
                System.out.print(a[j] + " ");
            System.out.println();
        }

        public void insert(long elem){
            a[nElems] = elem;
            nElems++;
        }

        public boolean delete(long elem){
            int j;
            for (j = 0; j < nElems; j++)
                if (a[j] == elem)
                    break;
            if (j == nElems)
                return false;
            else {
                for (; j < nElems - 1; j++)
                    a[j] = a[j + 1];
                nElems--;
                return true;
            }
        }

        public int find(long searchKey) {
            int lowerBound = 0;
            int highBound = nElems-1;
            int curPos = (lowerBound+highBound)/2;

            while (true) {
                if (a[curPos] == searchKey)
                    return curPos;
                else if (lowerBound > highBound)
                    return -1;
                else
                    if (a[curPos] > searchKey)
                        highBound = curPos-1;
                    else
                        lowerBound = curPos+1;
            }
        }

        public void bublSort() {
            for (int i = nElems-1; i > 0; i--)
                for (int j = 0; j < i; j++)
                    if (a[j]<a[i]) {
                        long temp;
                        temp = a[j];
                        a[j] = a[i];
                        a[i] = temp;
                    }
        }

        public void selectSort() {
            int ptr, i, j;
            long temp;
            ptr = 0;
            for (i = 0; i < nElems-1; i++) {
                ptr = i;
                for (j = i + 1; j < nElems; j++)
                    if (a[j] < a[ptr])
                        ptr = j;
                temp = a[i];
                a[i] = a[ptr];
                a[ptr] = temp;
            }
        }

        public void insertSort() {
            long temp;
            int j, i;
            for (i = 1; i < nElems; i++) {
                temp = a[i];
                j = i;
                while (j > 0 && a[j - 1] >= temp) {
                    a[j] = a[j-1];
                    j--;
                }
                a[j] = temp;
            }
        }
    }

    public static void main(String[] arg) {
        OrdArray ordArray = new OrdArray(100);

        for (int i = 0; i < 25; i++) {
            ordArray.insert(7);
            ordArray.insert(5);
            ordArray.insert(3);
            ordArray.insert(1);
        }
        ordArray.display();
        long start = new Date().getTime();
        ordArray.insertSort();
        long end = new Date().getTime();
        long time = end-start;
        ordArray.display();
        System.out.println(time);
    }
}

