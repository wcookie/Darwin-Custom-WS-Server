using System.Net.Sockets;
using System.Net;
using System;

class Server
{
    public static void Main()
    {
        TcpListener server = new TcpListener(IPAddress.Parse("192.168.0.16"), 80);

        server.Start();
        Console.WriteLine("Server has started on 127.0.0.1:8126.{0}Waiting for a connection...", Environment.NewLine);

       // TcpClient client = server.AcceptTcpClient();

       // Console.WriteLine("A client connected.");
        Byte[] bytes = new Byte[256];
        String data = null;
        try {
        // Enter the listening loop.
        while (true)
        {
            Console.Write("Waiting for a connection... ");

            // Perform a blocking call to accept requests.
            // You could also user server.AcceptSocket() here.
            TcpClient client = server.AcceptTcpClient();
            Console.WriteLine("Connected!");

            data = null;

            // Get a stream object for reading and writing
            NetworkStream stream = client.GetStream();

            int i;

            // Loop to receive all the data sent by the client.
            while ((i = stream.Read(bytes, 0, bytes.Length)) != 0)
            {
                // Translate data bytes to a ASCII string.
                data = System.Text.Encoding.ASCII.GetString(bytes, 0, i);
                Console.WriteLine("Received: {0}", data);

                // Process the data sent by the client.
                data = data.ToUpper();

                byte[] msg = System.Text.Encoding.ASCII.GetBytes(data);

                // Send back a response.
                stream.Write(msg, 0, msg.Length);
                Console.WriteLine("Sent: {0}", data);
            }

            // Shutdown and end connection
            client.Close();
        }
    }
    catch(SocketException e)
    {
      Console.WriteLine("SocketException: {0}", e);
    }
    finally
    {
       // Stop listening for new clients.
       server.Stop();
    }


    Console.WriteLine("\nHit enter to continue...");
    Console.Read();
  }

    }
