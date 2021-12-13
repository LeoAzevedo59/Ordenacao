# Ordenacao
Script para cortar elementos, ordenar e realizar a contagem de elementos repetidos


using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace PrimeiroProjeto
{
    class Program
    {
        public static List<registros> resultado { get; set; } = new List<registros>();
        public class registros
        {
            public string Nome { get; set; }
            public int Quantidade { get; set; }

            internal object OrderByDescending(Func<object, object> p)
            {
                throw new NotImplementedException();
            }
        }

        static void Main()
        {

            string text = System.IO.File.ReadAllText(@"C:\Users\leonardo.azevedo\Desktop\api.txt");

            string[] corte = text.Split(',');

            registros objregistro = new registros();
            objregistro.Nome = "ERROSIMULADO";
            objregistro.Quantidade = 1;
            resultado.Add(objregistro);

            foreach (var item in corte)
            {
                AdicionarElemento(item.Replace(" ", "")
                                      .Replace("\n", "")
                                      .Replace("\r", "")
                                      .Replace("n/a", "N/D")
                                      .Replace("n/d", "N/D")
                                      .Replace("N/Dchei", "N/D")
                                      .Replace("ÑACHEI", "N/D"));
            }

            resultado.RemoveAll(x => x.Nome == "ERROSIMULADO");

            foreach (var print in resultado)
            {
                Console.WriteLine(print.Nome + " " + print.Quantidade);

            }

        }

        private static void Sort()
        {
            throw new NotImplementedException();
        }

        public static void AdicionarElemento(string nome)
        {
            var index = resultado.Select((registro, index) => (registro, index)).FirstOrDefault (x => x.registro.Nome == nome).index;
            if (index > 0)
            {
                resultado.Where(w => w.Nome == nome).ToList().ForEach(i => i.Quantidade ++);
            }
            else
            {
                registros objregistro = new registros();
                objregistro.Nome = nome;
                objregistro.Quantidade = 1;
                resultado.Add(objregistro);
            }
        }
    }
}
