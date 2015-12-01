
GangliaAPI for JAVA:

The Ganglia API is a small standalone java application that takes XML data from a number of Ganglia gmetad processes and presents a useful API of the most recently received data.

This is designed to be part of our wider monitoring and metrics framework.

What I want to say

The ganglia gmetad API leaves something to be desired. It polls the gmetad thread to get current cluster metrics, keeping the latest results in memory.

Requirements and assumptions:

You need to add "org.dom4j" package to your project if you want to recompile.

Usage and exmple code:

public static void main(String [] args){
		
		RemoteReader httpAccess = new RemoteReader();
		
		String input =httpAccess.SendRequest();
		
		MetricsRetrieve metricsRetrive = new MetricsRetrieve();
		
		metricsRetrive.Parse(input);
		
		System.out.print(metricsRetrive.getClusterNumber());
		
		List<Metric> metrics = metricsRetrive.getMetricsByNameInCluster("jassion", "localhost");
		
		for(Metric metric  : metrics){
			
			System.out.println("name:  "+metric.getName());
			
			System.out.println("value: "+metric.getValue());
			
			System.out.println("type: "+metric.getType());
			
		}
		
		return ;
		
	}
	
	
RemoteReader try to connect the remote gmetad thread by predefined ip and port(default is 27.0.0.1:8651) which depends on your gnaglia setting. MetricsRetrieve analysis the raw input data and encapsulate them in for of Metric struct.


If you have any problems about my code, please feel free to contact me: ynjassionchen@gmail.com
