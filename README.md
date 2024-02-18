# Időkomplexitás mérése

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace rendezesek
{
    class Program
    {
        static void Main(string[] args)
        {
            
            int[] array = new int[100000];
            Random rand = new Random();
            for (int i = 0; i < array.Length; i++)
            {
                array[i] = rand.Next();
            }
            DateTime startTime = DateTime.Now;

            Task bubbleSortTask = Task.Run(() =>
            {
                BubbleSort(array, startTime);
            });

            Task insertionSortTask = Task.Run(() =>
            {
                InsertionSort(array, startTime);
            });

            Task selectionSortTask = Task.Run(() =>
            {
                SelectionSort(array, startTime);
            });

            Task defaultSortTask = Task.Run(() =>
            {
                DefaultSort(array, startTime);
            });
            Console.ReadKey();
        }

        private static void DefaultSort(int[] array, DateTime startTime)
        {
            array.ToList().Sort();
            Console.WriteLine($"default: {DateTime.Now.Subtract(startTime).TotalSeconds}");
        }

        public static void BubbleSort(int[] arr, DateTime startTime)
        {
            int n = arr.Length;
            for (int i = 0; i < n - 1; i++)
            {
                for (int j = 0; j < n - i - 1; j++)
                {
                    if (arr[j] > arr[j + 1])
                    {
                        int temp = arr[j];
                        arr[j] = arr[j + 1];
                        arr[j + 1] = temp;
                    }
                }
            }
            Console.WriteLine($"bubble: {DateTime.Now.Subtract(startTime).TotalSeconds}");
        }
        public static void InsertionSort(int[] arr, DateTime startTime)
        {
            int n = arr.Length;
            for (int i = 1; i < n; ++i)
            {
                int key = arr[i];
                int j = i - 1;

                while (j >= 0 && arr[j] > key)
                {
                    arr[j + 1] = arr[j];
                    j = j - 1;
                }
                arr[j + 1] = key;
            }
            Console.WriteLine($"insertion: {DateTime.Now.Subtract(startTime).TotalSeconds}");
        }
        public static void SelectionSort(int[] arr, DateTime startTime)
        {
            int n = arr.Length;

            for (int i = 0; i < n - 1; i++)
            {
                int min_idx = i;
                for (int j = i + 1; j < n; j++)
                {
                    if (arr[j] < arr[min_idx])
                    {
                        min_idx = j;
                    }
                }

                int temp = arr[min_idx];
                arr[min_idx] = arr[i];
                arr[i] = temp;
            }
            Console.WriteLine($"selection: {DateTime.Now.Subtract(startTime).TotalSeconds}");
        }

    }
}
```
