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

        public void swap(int first, int second) {
            long temp;
            temp = a[first];
            a[first] = a[second];
            a[second] = temp;
        }

        public void bublSort() {
            for(int out = nElems-1; out > 0; out--)
                for (int in = 0; in < out; in++)
                    if (a[in] > a[out])
                        swap(in,out);
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

        public long getElem(int index) {
            return a[index];
        }

        public OrdArray merge(OrdArray b) {
            int newSize = getSize()+b.getSize();
            OrdArray c = new OrdArray(newSize);
            for (int i = 0; i < getSize(); i++)
                c.insert(a[i]);
            for (int i = 0; i < b.getSize(); i++)
                c.insert(b.getElem(i));
            return c;
        }

        public void noDups() {
            int count = 0;
            for (int i = 0; i < nElems-1; i++)
                for (int j = i+1; j < nElems; j++)
                    if (a[j] == a[i]) {
                        for (int k = j; k < nElems - 1; k++)
                            a[k] = a[k + 1];
                        nElems--;
                    }
        }
    }

    public static void main(String[] arg) {
        long start = new Date().getTime();
        System.out.println(new Date().getTime());
        OrdArray ordArray = new OrdArray(5);

        ordArray.insert(7);
        ordArray.insert(5);
        ordArray.insert(3);
        ordArray.insert(1);
        ordArray.insert(1);
        ordArray.display();
        System.out.println(ordArray.getSize());
        System.out.println(ordArray.find(3));
        ordArray.delete(5);
        ordArray.display();
        System.out.println(ordArray.getSize());

        ordArray.insert(5);

        OrdArray newOrdArray = new OrdArray(3);
        newOrdArray.insert(2);
        newOrdArray.insert(4);
        newOrdArray.insert(6);
        OrdArray c = ordArray.merge(newOrdArray);
        c.display();
        c.noDups();
        c.display();
        c.bublSort();
        c.display();

        long end = new Date().getTime();
        System.out.println(end-start);
    }

}
