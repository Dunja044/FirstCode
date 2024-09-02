using System.Security.Cryptography.X509Certificates;
using System.Text.Json;
using System.Text.RegularExpressions;

namespace kosarkaski_turnir
{
    internal class Program
    {
        static void Main(string[] args)
        {

            if (File.Exists("..\\..\\..\\groups.json"))
            {
                using (FileStream fs = new FileStream("..\\..\\..\\groups.json", FileMode.Open))
                {
                    StreamReader sr = new StreamReader(fs);

                    string grupe = sr.ReadToEnd();



                    KosarkaskeGrupe kGrupe =
            JsonSerializer.Deserialize<KosarkaskeGrupe>(grupe);


                    int NajmanjiRank = 1;


                    for (int i = 0; i < kGrupe.A.Count; i++)
                    {
                        if (kGrupe.A[i].FIBARanking > NajmanjiRank)
                            NajmanjiRank = kGrupe.A[i].FIBARanking;
                    }

                    for (int i = 0; i < kGrupe.B.Count; i++)
                    {
                        if (kGrupe.B[i].FIBARanking > NajmanjiRank)
                            NajmanjiRank = kGrupe.B[i].FIBARanking;
                    }

                    for (int i = 0; i < kGrupe.C.Count; i++)
                    {
                        if (kGrupe.C[i].FIBARanking > NajmanjiRank)
                            NajmanjiRank = kGrupe.C[i].FIBARanking;
                    }

                    NajmanjiRank = NajmanjiRank + 5;
                    int a1;
                    int a2;
                    int razlika;

                    for (int i = 0; i < kGrupe.A.Count - 1; i++)
                        for (int j = i + 1; j < kGrupe.A.Count; j++)
                        {
                            Console.WriteLine(kGrupe.A[i].Team);
                            Console.WriteLine(kGrupe.A[j].Team);

                            if (kGrupe.A[i].FIBARanking > kGrupe.A[j].FIBARanking)
                            {
                                a2 = NajmanjiRank + (kGrupe.A[i].FIBARanking - kGrupe.A[j].FIBARanking);
                                a1 = NajmanjiRank - (kGrupe.A[i].FIBARanking - kGrupe.A[j].FIBARanking);
                            }
                            else
                            {
                                a1 = NajmanjiRank + (kGrupe.A[j].FIBARanking - kGrupe.A[i].FIBARanking);
                                a2 = NajmanjiRank - (kGrupe.A[j].FIBARanking - kGrupe.A[i].FIBARanking);
                            }



                            Console.WriteLine(a1.ToString());
                            Console.WriteLine(a2.ToString());

                            Console.WriteLine("---");


                        }

                    NajmanjiRank = NajmanjiRank + 5;
                    int b1;
                    int b2;
                    int razlika1;



                    for (int i = 0; i < kGrupe.B.Count - 1; i++)
                    for (int j = i + 1; j < kGrupe.B.Count; j++)
                        {
                            Console.WriteLine(kGrupe.B[i].Team);
                            Console.WriteLine(kGrupe.B[j].Team);

                            if(kGrupe.A[i].FIBARanking > kGrupe.B[j].FIBARanking)
                            {
                                b2 = NajmanjiRank + (kGrupe.B[i].FIBARanking - kGrupe.B[j].FIBARanking);
                                b1 = NajmanjiRank - (kGrupe.B[i].FIBARanking - kGrupe.B[j].FIBARanking);

                            }    
                            else
                            {
                                b1 = NajmanjiRank + (kGrupe.B[j].FIBARanking - kGrupe.B[i].FIBARanking);
                                b2 = NajmanjiRank - (kGrupe.B[j].FIBARanking - kGrupe.B[i].FIBARanking);

                            }


                            Console.WriteLine(b1.ToString());
                            Console.WriteLine(b2.ToString());

                            Console.WriteLine("---");



                        }


                    NajmanjiRank = NajmanjiRank + 5;
                    int c1;
                    int c2;
                    int razlika2;




                    for (int i = 0; i < kGrupe.C.Count - 1; i++)
                        for (int j = i + 1; j < kGrupe.C.Count; j++)
                        {
                            Console.WriteLine(kGrupe.C[i].Team);
                            Console.WriteLine(kGrupe.C[j].Team);

                            if (kGrupe.A[i].FIBARanking > kGrupe.C[j].FIBARanking)
                            {
                                c2 = NajmanjiRank + (kGrupe.C[i].FIBARanking - kGrupe.C[j].FIBARanking);
                                c1 = NajmanjiRank - (kGrupe.C[i].FIBARanking - kGrupe.C[j].FIBARanking);

                            }
                            else
                            {
                                c1 = NajmanjiRank + (kGrupe.C[j].FIBARanking - kGrupe.C[i].FIBARanking);
                                c2 = NajmanjiRank - (kGrupe.C[j].FIBARanking - kGrupe.C[i].FIBARanking);

                            }


                            Console.WriteLine(c1.ToString());
                            Console.WriteLine(c2.ToString());

                            Console.WriteLine("---");



                          

                        }


                    var groupA = new List<Team>
                    {
                         new Team { Name = "Kanada", Wins = 3, Losses = 0, Points = 6, ScoredPoints = 267, ConcededPoints = 247 },
                         new Team { Name = "Australija", Wins = 2, Losses = 1, Points = 4, ScoredPoints = 246, ConcededPoints = 250 },
                         new Team { Name = "Grčka", Wins = 2, Losses = 1, Points = 4, ScoredPoints = 233, ConcededPoints = 241 },
                         new Team { Name = "Španija", Wins = 2, Losses = 1, Points = 4, ScoredPoints = 249, ConcededPoints = 257 }
                    };

                   
                    Console.WriteLine("Konačan plasman u grupama:");
                    

                    var quarterfinals = new List<(Team, Team)>
                    {
                        (groupA[1], groupA[2]), 
                        (groupA[0], groupA[3])  
                    };

                    Console.WriteLine("\nEliminaciona faza:");
                    DisplayQuarterfinals(quarterfinals);

                    var exhibitionResults = new Dictionary<string, List<(int, int)>>
                    {
                         { "Kanada", new List<(int, int)> { (85, 79), (90, 85) } },
                         { "Australija", new List<(int, int)> { (92, 80), (88, 82) } },
                         { "Grčka", new List<(int, int)> { (78, 85), (83, 79) } },
                        { "Španija", new List<(int, int)> { (80, 92), (85, 88) } }
                    };

                    Console.WriteLine("\nForma timova:");
                    CalculateTeamForm(groupA, exhibitionResults);

                    foreach (var team in groupA)
                    {
                        Console.WriteLine($"{team.Name}: {team.Form:F2}");




                    }


                     static void DisplayGroupStandings(string groupName, List<Team> teams)
                    {
                        Console.WriteLine($"{groupName} (Ime - pobede/porazi/bodovi/postignuti koševi/primljeni koševi/koš razlika):");
                    }

                     static void DisplayQuarterfinals(List<(Team, Team)> matchups)
                    {
                        foreach (var (team1, team2) in matchups)
                        {
                            Console.WriteLine($"{team1.Name} - {team2.Name}");
                        }
                    }



                     static void CalculateTeamForm(List<Team> teams, Dictionary<string, List<(int, int)>> exhibitionResults)
                    {
                        foreach (var team in teams)
                        {
                            if (exhibitionResults.TryGetValue(team.Name, out var results))
                            {
                                double form = results.Average(result => (double)result.Item1 / result.Item2);
                                team.Form = form;
                            }
                        }
                    }

                         
using kosarkaski_turnir;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace kosarkaski_turnir
{
    public class Tim
    {
        public string Team { get; set; }
        public string ISOCode { get; set; }
        public int FIBARanking { get; set; }
    }

    public class KosarkaskeGrupe
    {
        public List<Tim> A { get; set; }
        public List<Tim> B { get; set; }
        public List<Tim> C { get; set; }

    }
}
  
public class Team
{
    public string Name { get; set; }
    public int Wins { get; set; }
    public int Losses { get; set; }
    public int Points { get; set; }
    public int ScoredPoints { get; set; }
    public int ConcededPoints { get; set; }
    public int PointDifference => ScoredPoints - ConcededPoints;
    public double Form { get; set; }
}



                        }
            }

        }
    }
}
