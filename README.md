# cis7-extra-credit

#include <iostream>
#include <string>
#include <vector>
using namespace std;

void addNode(int, string);
void addEdge(string, string);
void highestDegree();
void isoVertice();
bool isolatedVertice();
void loops();
void gConnected();
void gComplete();

struct node
{
	string name;
	int id;
	int connections;
};

vector <node> vertices;
vector <int> edgeFrom;
vector <int> edgeTo;


int main()
{
	int counter = 0;
	string newNode;
	string node1;
	string node2;
	int answer;
	bool exit = false;
	do
	{
		cout << "Please choose one option below. \n";
		cout << "1. Add vertice \n2. Add edge \n3. Highest Degree \n4. Isloated vertice \n5. Loops \n6. Connected Graph? \n7. Complete Graph?" << endl;
		cin >> answer;
		while (answer < 1 || answer > 7)
		{
			cout << "Pick one of the options..." << endl;
			cin >> answer;
		}

		switch (answer)
		{
		case 1:
			cout << "Enter the name of the new vertice. : ";
			cin >> newNode;
			addNode(counter, newNode);
			counter++;
			cout << "Done." << endl;

			break;
		case 2: cout << '2';
			cout << "Enter the name of the first vertice : ";
			cin >> node1;
			cout << "Enter the name of the second vertice : ";
			cin >> node2;
			addEdge(node1, node2);
			cout << "Done." << endl;

			break;
		case 3:
			highestDegree();

		case 4:
			isoVertice();

		case 5:
			loops();

		case 6:
			gConnected();

		case 7:
			gComplete();

		}
	} while (exit == false);



	return 0;
}


void addNode(int counter, string newNode)
{
	node bleh;
	bleh.id = counter;
	bleh.name = newNode;
	bleh.connections = 0;

	vertices.push_back(bleh);
}

void addEdge(string node1, string node2)
{
	int id1;
	int id2;

	for (int i = 0; i < vertices.size(); i++)
	{
		if (vertices[i].name == node1)
		{
			id1 = vertices[i].id;
			vertices[i].connections++;
		}

	}

	for (int i = 0; i < vertices.size(); i++)
	{
		if (vertices[i].name == node2)
		{
			id2 = vertices[i].id;
		}
		else if (id1 != id2)
		{
			vertices[i].connections++;
		}
	}
	if (id1 < id2)
	{
		edgeFrom.push_back(id1);
		edgeTo.push_back(id2);
	}
	else
	{
		edgeTo.push_back(id1);
		edgeFrom.push_back(id2);
	}
}

void highestDegree()
{
	int highI = 0;
	for (int i = 0; i < vertices.size(); i++)
	{
		if (highI < vertices[i].connections)
		{
			highI = vertices[i].connections;
		}
	}

	cout << "The vertex with the highest degree is " << vertices[highI].name << endl;
}

void isoVertice()
{
	vector <node> noC;
	for (int i = 0; i < vertices.size(); i++)
	{
		if (vertices[i].connections == 0)
		{
			noC.push_back(vertices[i]);
		}
	}

	if (noC.size() == 0)
	{
		cout << "There are no isolated vertices." << endl;
	}
	else
	{
		for (int i = 0; i < noC.size(); i++)
		{
			cout << noC[i].name << " \n";
		}
	}
}

void loops()
{
	int loop = 0;
	for (int i = 0; i < edgeFrom.size(); i++)
	{
		if (edgeFrom[i] == edgeTo[i])
		{
			loop++;
		}
	}

	cout << "There are " << loop << " loops in this graph." << endl;

}

void gConnected()
{
	bool connected = false;
	bool con = false;
	int a = 0;
	for (int i = 0; i < edgeFrom.size(); i++)
	{
		for (int j = 0; j < edgeTo.size(); i++)
		{
			int f = 0;
			a = 0;

			while (f < edgeTo.size())
			{
				if (edgeFrom[i] == edgeTo[i] + a)
				{
					connected = true;
				}
				f++;
				a++;
			}
			if (connected == true)
			{
				con = true;
			}
			else
			{
				con = false;
			}

			a++;
		}
		a = 0;
	}
	if (con == true)
	{
		cout << "The graph is connected." << endl;
	}
	else
	{
		cout << "The graph is not connected" << endl;
	}

}

void gComplete()
{
	bool connected = false;
	bool con = false;
	int a = 0;
	for (int i = 0; i < edgeFrom.size(); i++)
	{
		for (int j = 0; j < edgeTo.size(); i++)
		{
			int f = 0;
			a = 0;

			while (f < edgeTo.size())
			{
				if (edgeFrom[i] == edgeTo[i] + a)
				{
					connected = true;
				}
				f++;
				a++;
			}
			if (connected == true)
			{
				con = true;
			}
			else
			{
				con = false;
			}

			a++;
		}
		a = 0;
	}
	if (isolatedVertice() == true)
	{
		con = false;
	}
	if (con == true)
	{
		cout << "The graph is complete." << endl;
	}
	else
	{
		cout << "The graph is not complete" << endl;
	}

}

bool isolatedVertice()
{
	bool iso = false;
	vector <node> noC;
	for (int i = 0; i < vertices.size(); i++)
	{
		if (vertices[i].connections == 0)
		{
			noC.push_back(vertices[i]);
		}
	}

	if (noC.size() == 0)
	{
		iso = false;
	}
	else
	{
		for (int i = 0; i < noC.size(); i++)
		{
			iso = true;
		}
	}
	return iso;
}
