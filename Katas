using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Numerics;
using System.Runtime.Remoting.Messaging;
using System.Security.Cryptography;
using System.Security.Principal;
using System.Text.RegularExpressions;
using System.Text;
using System.Threading.Tasks;
using System.Xml.Schema;

namespace CodeWarsTester
{
	public static class Kata
	{
		#region AwesomeMultiplication

		public static string Multiplication(string one, string two)
		{
			var iteration = 0;
			//список длинной в количество знаков первого числа, и содержащий по 1 цифре в каждом ноде
			var first = one.ToCharArray().Select(c => Convert.ToInt32(c.ToString())).ToList(); 
			//аналогично для второго числа
			var second = two.ToCharArray().Select(c => Convert.ToInt32(c.ToString())).ToList();
			//заготовка для результирующего списка произведения
			var result = Enumerable.Repeat(0, first.Count + second.Count).ToList();
			int k = result.Count;
			//умножение
			for (int i = first.Count - 1; i >= 0; i--)
			{
				//промежуточный список в который сохраняется результат перемножения выбранной (изначально последней)
				//цифры первого множителя с каждой цифрой второго
				var temp = new List<int>();
				for (int j = second.Count - 1; j >= 0; j--)
				{
					temp.Add(first[i] * second[j]);
					iteration++;
				}
				//т.к.метод Add добавляет в конец (получаем последовательность наоборот), реверсируем список (первое место для рефакторинга)
				temp.Reverse();
				//почленно суммируем и записываем промежуточный список в результирующий с соответствующим смещением
				for (int z = temp.Count - 1; z >= 0; z--)
				{
					var a = k - (temp.Count - z);
					result[a] += temp[z];
					iteration++;
				}
				iteration++;
				//корректировка смещения
				k--;
			}
			//оставляем по одной цифре в ноде результирующего списка перенося остаток по возрастанию выше, до 0 нода
			for (int i = result.Count - 1; i >= 0; i--)
			{
				//здесь остаток остается неизменным, т.к. это не влияет на корректный вывод ответа
				if (i == 0) break;
				//число в ноде
				var temp = result[i].ToString();
				//последняя цифра числа, которая останется в ноде
				var last = Convert.ToInt32(temp[temp.Length - 1].ToString());
				//удаление цифры из числа и уменьшение его на порядок - остаток
				var y = temp.Remove(temp.Length - 1);
				//если число равно 0 ничего переносить не нужно
				if (string.IsNullOrEmpty(y)) continue;
				//перенос остатка в следующмй нод
				result[i - 1] += int.Parse(y);
				//сохранение в текущем ноде последней цифры
				result[i] = last;
				iteration++;
			}
			var sb = new StringBuilder();
			#region RemoveZerosFromBeginning
			if (result[0] == 0)
			{
				var zero = 0;
				while (zero == 0)
				{
					result.RemoveAt(0);
					zero = result[0];
					iteration++;
				}
			}
			#endregion
			#region ConverToString
			for (int i = 0; i < result.Count; i++)
			{
				sb.Append(result[i]);
				iteration++;
			}
			#endregion

			var answer = $"result = {sb.ToString()} \n iterations made:{iteration}";
			return answer;
		}
		#endregion
		#region MorseCodeDecoderPartOne

		public static string Decode(string code)
		{
			#region MorzeDictionary
			var dict = new Dictionary<string, string>()
			{
				{"...---...", "SOS" },
				{".-", "A"},
				{"-...", "B"},
				{"-.-.", "C"},
				{"-..", "D"},
				{".", "E"},
				{"..-.", "F"},
				{"--.", "G"},
				{"....", "H"},
				{"..", "I"},
				{".---", "J"},
				{"-.-", "K"},
				{".-..", "L"},
				{"--", "M"},
				{"-.", "N"},
				{"---", "O"},
				{".--.", "P"},
				{"--.-", "Q"},
				{".-.", "R"},
				{"...", "S"},
				{"-", "T"},
				{"..-", "U"},
				{"...-", "V"},
				{".--", "W"},
				{"-..-", "X"},
				{"-.--", "Y"},
				{"--..", "Z"},
				{"   ", " "},
				{".----", "1"},
				{"..---", "2"},
				{"...--", "3"},
				{"....-", "4"},
				{".....", "5"},
				{"-....", "6"},
				{"--...", "7"},
				{"---..", "8"},
				{"----.", "9"},
				{"-----", "0" },
				{".-.-.-", "." },
				{"-.-.--", "!" }
			};
			#endregion
			var temp = new StringBuilder();
			code = code.Trim();
			var letters = (from object s in Regex.Matches(code, "[.-]{1,9}|\\s{3}") select s.ToString()).ToList();
			foreach (var letter in letters) { var x = letter == "   " ? temp.Append(" ") : temp.Append(dict[letter]); }
			return temp.ToString();
			//return string.Concat(morseCode.Trim().Replace("   "," X ").Split().Select(x=>x!="X" ? MorseCode.Get(x) : " "));

		}

		//private static List<string> Func(string word) => (from object s in Regex.Matches(word, "\\s?[.-]*") select s.ToString()).ToList();
		#endregion
		//TODO
		#region PhoneDirectory
		//public static string Phone(string strng, string num)
		//{
		//    var matches = Regex.Matches(strng, num);
		//    if (matches.Count > 1) return $"Error => Too many people: {num}";
		//    if (matches.Count < 1) return $"Error => Not found: {num}";
		//    var name = Regex.Match
		//}
		#endregion
		#region SumFrom1toN
		public static long Total(long n) => (1 + n) * n / 2;
		#endregion
		#region JohnSnowParents
		public static string JohnSnowParents(string dad, string mom)
		{
			return dad == "Rhaegar Targaryen" && mom == "Lyanna Stark"
				? "Jon Snow you deserve the throne"
				: "You know nothing, Jon Snow";
		}
		#endregion
		#region FizzBuzz
		public static String CalcFizzBuzz(int n)
		{
			return n == 0 ? "" : n % 15 == 0 ? "Fizz Buzz" : n % 5 == 0 ? "Fizz" : n % 3 == 0 ? "Buzz" : n.ToString();
		}
		#endregion
		#region GetFactorialFunction
		public static Func<int, int> GetFactorialFunction() => (x) => { int p = 1; for (int i = 1; i <= x; i++) p *= i; return p; };
		#endregion
		#region EgyptianFractions

		public static string Decompose(string nrStr, string drStr)
		{
			var nom = BigInteger.Parse(nrStr);
			if (nom == 0) return "[]";
			var den = BigInteger.Parse(drStr);
			if (nom % den == 0) return $"[{nom / den}]";
			var divided = DecomposeHelper(nom, den);
			if (divided[0] == 1) return $"[{divided[0]}/{divided[1]}]";
			StringBuilder result = new StringBuilder();
			List<BigInteger> second;
			result.Append("[");
			do
			{
				var first = Convert.ToInt32(Math.Ceiling((decimal)den / (decimal)nom));
				second = DecomposeHelper(FirstNom(den, nom), SecondNom(den, (int)nom));
				if (first == 1)
				{
					result.Append(first);
				}
				else
				{
					result.Append($"1/{first}");
				}
				result.Append(", ");
				if (second[0] == 1)
				{
					result.Append($"1/{second[1]}]");
				}
				nom = second[0];
				den = second[1];
			} while (second[0] != 1);
			return result.ToString();
		}

		static List<BigInteger> DecomposeHelper(BigInteger nom, BigInteger denom)
		{
			var result = new List<BigInteger>();
			var x = BigInteger.GreatestCommonDivisor(nom, denom);
			result.Add(nom / x);
			result.Add(denom / x);
			return result;
		}

		static BigInteger FirstNom(BigInteger a, BigInteger b)
		{
			return (-a) % b + b;
		}

		static BigInteger SecondNom(BigInteger a, int b)
		{
			return a * Convert.ToInt32(Math.Ceiling((double)a / b));
		}
		#endregion
		#region DescendingOrder
		public static int DescendingOrder(int num)
		{
			return int.Parse(string.Concat(num.ToString().OrderByDescending(c => c)));
		}
		#endregion
		#region SpeedControl

		public static int Gps(int s, double[] x)
		{
			return x.Length < 2 ? 0 : (int)(x.Select((n, i) => (i == 0 ? n : x[i] - x[i - 1])).Max() / s * 3600);
			//double maxCut = 0;
			//for (int i = 1; i < x.Length; i++)
			//{
			//    maxCut<Math.Abs(x[i]-x[i-1])?maxCut= Math.Abs(x[i] - x[i - 1])
			//}
			//return Convert.ToInt32(maxCut / s * 3600);
		}
		#endregion
		#region MinutesInTimeString
		public static int MinutesInTimeString(string x)
		{
			return x.Split(':').Sum((s) => x.IndexOf(s) < 1 ? int.Parse(s) * 60 : int.Parse(s));
		}
		#endregion
		#region FindTheCapitals

		public static int[] Capitals(string word)
		{

			//List<int> capitals = new List<int>();
			//for (int i = 0; i < word.Length; i++)
			//{
			//	if(Regex.IsMatch(word[i].ToString(),"[A-Z]")) capitals.Add(i);
			//}
			//return capitals.ToArray();
			//return word.ToCharArray()
			//	.Select((c, index) => new {CharAtIndex = c, Idx = index})
			//	.Where(indexedList => char.IsUpper(indexedList.CharAtIndex))
			//	.Select(selected => selected.Idx)
			//	.ToArray();
			//The BEST: 
			return word.Select((c, i) => char.IsUpper(c) ? i : -1).Where(i => i >= 0).ToArray();
		}

		#endregion
		//TODO
		#region GapInPrimes

		#endregion
		#region Vasya-Clerk
		public static string Tickets(int[] peopleInLine)
		{
			var vasia = new Dictionary<int, int> { { 25, 0 }, { 50, 0 }, { 100, 0 } };
			if (peopleInLine[0] != 25)
			{
				return "NO";
			}
			vasia[peopleInLine[0]]++;
			for (int i = 1; i < peopleInLine.Length; i++)
			{
				switch (peopleInLine[i])
				{
					case 25:
						vasia[peopleInLine[i]]++;
						break;
					case 50:
						if (vasia[25] == 0) return "NO";
						vasia[peopleInLine[i]]++;
						vasia[peopleInLine[i] - 25]--;
						break;
					case 100:
						if (vasia[25] == 0) return "NO";
						if (vasia[50] >= 1 && vasia[25] != 0)
						{
							vasia[25]--;
							vasia[50]--;
							vasia[peopleInLine[i]]++;
							break;
						}
						if (vasia[25] >= 3)
						{
							vasia[25] -= 3;
							vasia[peopleInLine[i]]++;
							break;
						}
						return "NO";
				}
			}
			return "YES";
		}
		#endregion
		#region AreYouPlayingBanjo?
		public static string AreYouPlayingBanjo(string name)
		{
			//Implement me
			return Regex.IsMatch(name[0].ToString(), "[Rr]") ? $"{name} plays banjo" : $"{name} does not play banjo";
		}
		#endregion
		#region GrowthOfThePopulation
		public static int NbYear(int p0, double percent, int aug, int p)
		{
			int years = 0;
			percent = percent / 100;
			while (p0 < p)
			{
				p0 += (int)(p0 * percent + aug);
				years++;
			}
			return years;
		}
		#endregion
		#region Digitizer
		public static int[] Digitize(int number)
		{
			var temp = number.ToString().Reverse().ToArray();
			int[] result = new int[temp.Length];
			for (int i = 0; i < temp.Length; i++)
			{
				result[i] = int.Parse(temp[i].ToString());
			}
			return result;
			//Best practice : 
			//return n.ToString().ToArray().Select((c) => int.Parse(c.ToString())).Reverse().ToArray();
		}
		#endregion
		#region MaxDiffLength
		public static int Mxdiflg(string[] a1, string[] a2)
		{
			return a1.Length == 0 | a2.Length == 0 ? -1 : Math.Max(a1.Max(x => x.Length) - a2.Min(x => x.Length), a2.Max(x => x.Length) - a1.Min(x => x.Length));
		}
		#endregion //
		#region RemoveEveryOther
		public static object[] RemoveEveryOther(object[] arr)
		{
			return arr.Where((a, i) => i % 2 == 0).ToArray();
		}
		#endregion
		#region VowelShortcut
		public static string Shortcut(string input)
		{
			return Regex.Replace(input, "[aoiue]", "");
		}
		#endregion
		#region RemoveSmallest
		public static List<int> RemoveSmallest(List<int> numbers)
		{
			numbers.Remove(numbers.DefaultIfEmpty().Min());
			return numbers;
		}
		#endregion
		#region AddStrings
		public static int AddStrings(string numbers)
		{
			int sum = 0;
			foreach (var i in numbers.Split(','))
			{
				try
				{
					sum += int.Parse(i);
				}
				catch (FormatException) { continue; }
			}
			return sum;
		}
		#endregion
		#region SubtractSum
		public static string SubtractSum(int number)
		{
			do
			{
				int n = 0;
				string s = number.ToString();
				char[] numbers = s.ToCharArray();
				foreach (char c in numbers)
				{
					n += int.Parse(c.ToString());
				}
				number -= n;
			} while (number >= 100 && number != 0);
			string[] fruits = new string[] { "bla",
											 "kiwi",
											 "pear",
											 "kiwi",
											 "banana",
											 "melon",
											 "banana",
											 "melon",
											 "pineapple",
											 "apple",
											 "pineapple",
											 "cucumber",
											 "pineapple",
											 "cucumber",
											 "orange",
											 "grape",
											 "orange",
											 "grape",
											 "apple",
											 "grape",
											 "cherry",
											 "pear",
											 "cherry",
											 "pear",
											 "kiwi",
											 "banana",
											 "kiwi",
											 "apple",
											 "melon",
											 "banana",
											 "melon",
											 "pineapple",
											 "melon",
											 "pineapple",
											 "cucumber",
											 "orange",
											 "apple",
											 "orange",
											 "grape",
											 "orange",
											 "grape",
											 "cherry",
											 "pear",
											 "cherry",
											 "pear",
											 "apple",
											 "pear",
											 "kiwi",
											 "banana",
											 "kiwi",
											 "banana",
											 "melon",
											 "pineapple",
											 "melon",
											 "apple",
											 "cucumber",
											 "pineapple",
											 "cucumber",
											 "orange",
											 "cucumber",
											 "orange",
											 "grape",
											 "cherry",
											 "apple",
											 "cherry",
											 "pear",
											 "cherry",
											 "pear",
											 "kiwi",
											 "pear",
											 "kiwi",
											 "banana",
											 "apple",
											 "banana",
											 "melon",
											 "pineapple",
											 "melon",
											 "pineapple",
											 "cucumber",
											 "pineapple",
											 "cucumber",
											 "apple",
											 "grape",
											 "orange",
											 "grape",
											 "cherry",
											 "grape",
											 "cherry",
											 "pear",
											 "cherry",
											 "apple",
											 "kiwi",
											 "banana",
											 "kiwi",
											 "banana",
											 "melon",
											 "banana",
											 "melon",
											 "pineapple",
											 "apple",
											 "pineapple"
											};
			return fruits[number];
		}
		#endregion
		#region GetMiddle
		public static string GetMiddle(string s)
		{
			return s.Substring(s.Length / 2 - (1 - s.Length % 2), 2 - s.Length % 2);
		}
		#endregion
		#region CountSheeps
		public static int CountSheeps(bool[] sheeps)
		{
			return sheeps.Count(s => s);
		}
		#endregion
	}
}
