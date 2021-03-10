# Lambda_steam
package pack;
import java.util.ArrayList;
import java.util.List;
import java.util.Random;
import java.util.stream.Collectors;
public class test {
	public static void main(String []args)
	{
		Random rand = new Random();
		List<Score> pd = new ArrayList<Score>();
		for(int i = 0; i < 101; i++)
			pd.add(new Score(rand.nextInt(99999),rand.nextInt(2),rand.nextInt(9999),rand.nextInt(99)));
		
		
		pd.stream().map(b-> b.tax()).collect(Collectors.toList());
		pd.stream().map(b-> b.TotalPriceTex = b.TotalPrice+b.TotalPrice * (b.Tax/100)).collect(Collectors.toList());
		
		pd.stream().map(b-> b.vat()).collect(Collectors.toList());
		pd.stream().map(b-> b.Sum = b.TotalPriceTex+b.TotalPriceTex * (b.Vat/100)).collect(Collectors.toList());
		
		
		List<Score> pdNotex = pd.stream().filter(b -> b.Type == 1).collect(Collectors.toList());
		
		
		List<Score> pdTopTen = pd.stream().sorted((b1, b2) -> b2.Amount.compareTo(b1.Amount)).limit(10).collect(Collectors.toList());
		
		
		System.out.println("\nAll product");
		Header();
		pd.forEach(b -> b.ShowList());
		
		
		System.out.println("\nNo Tax product");
		Header();
		pdNotex.forEach(b -> b.ShowList());
		
		
		System.out.println("\nTop ten product");
		Header();
		pdTopTen.forEach(b -> b.ShowList());
		
		
	}
	static void Header()
	{
		
		System.out.println("|      ID     |      Type      |    Price    |     Amount   | Amount TotalPrice |    Tax   | Tax TotalPriceTex |     Vat    | TotalPriceTexVat |");
		
	}
}
class Score
{
	int ID;
	int Type;
	String TypeText;
	float Price;
	Integer Amount;
	float TotalPrice;
	float TotalPriceTex;
	float Tax = 0;
	float Vat = 0;
	float Sum = 0;
	Score(int ID, int Type, float Price, Integer Amount)
	{
		this.ID = ID;
		this.Type = Type;
		this.Price = Price;
		this.Amount = Amount;
		TotalPrice = Price*Amount ;
	}
	float tax()
	{
		if(Type == 0)
		{
			TypeText="Tax";
			Tax += 7;
		}else {
			TypeText="NoTax  ";
		}
		
		return Tax;
	}
	float vat()
	{
		if(TotalPriceTex > 100000)
		{
			Vat += 10;
		}else if(TotalPriceTex > 50000)
		{
			Vat += 5;
		}
		return Vat;
	}
	void ShowList()
	{
		System.out.format("|   %7d   |   %10s   |   %7.2f   |  %7d     |    %10.2f     |  %3.0f%%    |    %10.2f     |   %3.0f%%     |    %10.2f    |\n"
				,ID,TypeText,Price,Amount,TotalPrice,Tax,TotalPriceTex,Vat,Sum);
		
	}
}
