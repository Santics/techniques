# Jsoncpp myDoc



> ***What is Json?***

​	Json is a lightweight data interchange format.

~~~json
// Configuration options
{
    // Default encoding for text
    "encoding" : "UTF-8",
    
    // Plug-ins loaded at start-up
    "plug-ins" : [
        "python",
        "c++",  // trailing comment
        "ruby"
        ],
        
    // Tab indent size
    // (multi-line comment)
    "indent" : { /*embedded comment*/ "length" : 3, "use_space": true }
}
~~~



***



> ***How to use Jsoncpp?***

+ **Create & Print your Json file**

~~~c++
#include <iostream>
//remember to include this head
#include<json/json.h>

using std::cout;
using std::cin;
using std::endl;

int main(int argc, int** argv)
{
    //create fundamental json object
    //this object looks like a dictionary
    //we can ues string indexes to appoint one specific data item
	Json::Value root;
    
    //create and assign data item
	root["null"] = NULL;
	root["message"] = "OK";
	root["age"] = 52;
    //to assign multidata item
    //we ues append func
	root["array"].append("arr");
	root["array"].append(123);
	root["array"].append("fluxxxx!");

    
	Json::ValueType type = root.type();

    //print json doc in standard string form
	cout << root.toStyledString() << endl;
    
	cout << "root_type:" << type << endl;
    
    //print one specific data item
	cout << root["message"].asString() << endl;

	return 0;
}

~~~



![1](.\resource\1.PNG)



+ **Create Json object from a string**

  ~~~c++
  #include<iostream>
  #include<json/json.h>
  #include<string>
  
  using std::cout;
  using std::cin;
  using std::endl;
  using std::string;
  
  int main(int argc, int** argv)
  {
      const char* str = "{\"name\":\"maomao\",\"age\":18}";
      
      //build a CharReader implementation
      //we can use syntax like this --> builder["someproperty"]=somevalue
      //for example --> builder["emitUTF8"]=true; builder["collectComments"]=false;
      Json::CharReaderBuilder builder;
      //interface for reading JSON from a char array
      Json::CharReader* reader(builder.newCharReader());
      //basic old friend
      Json::Value root;
      //or std::string errs;
      JSONCPP_STRING errs;
      
      //there is another way to create root from stream
      //bool ok = Json::parseFromStream(builder,std::cin,&root,&errs);
      //bool ok = charreader -> parse(*charstart,*charend,&root,&errs);
      bool isOK = reader->parse(str, str + strlen(str), &root, &errs);
      
      //have no idea what is going on in the part
      if (isOK && errs.size() == 0)
      {
          //access to data node
          //upload_id = "UP000000" 
          string upload_id = root["uploadid"].asString();
          //access to data node，code = 100  
          int code = root["code"].asInt();    
      }
      //seriously? what did he do???
      
      delete reader;
      cout << root.toStyledString() << endl;
      cout << "name: " << root["name"].asString() << "age: "<< root["age"].asString()<< endl;
  
  	return 0;
  }
  ~~~

  

![2](.\resource\2.PNG)



+ **Transfer Json data to a file**

~~~c++
#include<iostream>
#include<fstream>
#include<json/json.h>
#include<string>

using std::cout;
using std::cin;
using std::endl;
using std::string;

int main(int argc, int** argv)
{
    Json::Value jsonRoot;
    Json::Value jsonItem;
    
    
    jsonItem["item1"].append("First");
    jsonItem["item1"].append("another First");
    jsonItem["item2"] = "Second";
    jsonRoot.append(jsonItem);
    //as the name suggests,it clears everything
    jsonItem.clear();
    jsonItem["First"] = "1";
    jsonItem["Second"] = "2";
    jsonItem["Third"] = "3";
    jsonRoot.append(jsonItem);

    
    std::ofstream ofs;
    ofs.open("testFile.json");
    ofs << jsonRoot.toStyledString() << endl;
    ofs.close();

    return 0;
}
~~~



+ **Extract Json from a file**

  ~~~c++
  #include<iostream>
  #include<fstream>
  #include<json/json.h>
  #include<string>
  
  using std::cout;
  using std::cin;
  using std::endl;
  using std::string;
  
  int main(int argc, int** argv)
  {
  	Json::CharReaderBuilder builder;
  	Json::Value root;
  	JSONCPP_STRING errs;
      root.clear();
  
  
  	std::ifstream ifs;
  	ifs.open("./resource/content.json");
  	bool parse_ok = Json::parseFromStream(builder, ifs, &root, &errs);
  	ifs.close();
      
      
  	if (!parse_ok)
  	{
  		cout << "Read File Error!" << endl;
  	}
  	else
  	{
  		cout << root.toStyledString() << endl;
  	}
  
      return 0;
  }
  ~~~

  