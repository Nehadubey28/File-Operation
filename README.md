# File-Operation
File Operation In Java

Reading JSon File
-------------------------------------
1) JACKSON Library (tutorial: https://www.javatpoint.com/jackson)
2) Gason Library
3) json-simple Library
-----------------------------------
Reading XML DOM
//DocumentBuilderFactory
//DocumentBuilder
//Document

DocumentBuilderFactory is a class in Java's XML processing API (part of the Java Standard Edition) used to create a DocumentBuilder, which can parse XML documents into a Document object.
This Document object represents the entire XML document and provides various methods to interact with its structure and data.

Key Points about DocumentBuilderFactory
Creation of DocumentBuilder: DocumentBuilderFactory is used to obtain a DocumentBuilder instance. This builder is then used to parse XML documents.
Configuration: DocumentBuilderFactory can be configured to control various parsing features, such as validation, ignoring comments, and whitespace handling.
Thread-Safety: DocumentBuilderFactory instances are not guaranteed to be thread-safe, so they should be used accordingly in multi-threaded applications.

Basic Steps to Parse XML with DocumentBuilderFactory
Obtain a DocumentBuilderFactory Instance: Create an instance of DocumentBuilderFactory.
Configure the Factory (Optional): Configure various settings on the DocumentBuilderFactory if needed.
Create a DocumentBuilder: Use the factory to create a DocumentBuilder.
Parse the XML Document: Use the DocumentBuilder to parse an XML file or input stream into a Document object.
Interact with the Document: Use the methods provided by the Document object to interact with the XML data.

Example Code
Here's a simple example demonstrating how to use DocumentBuilderFactory to parse an XML document:

import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.DocumentBuilder;
import org.w3c.dom.Document;
import java.io.File;
public class XMLParserExample {
    public static void main(String[] args) {
        try {
            // Step 1: Create a DocumentBuilderFactory
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            
            // Step 2: Configure the factory (optional)
            factory.setNamespaceAware(true);
            factory.setValidating(false);
            factory.setIgnoringElementContentWhitespace(true);

            // Step 3: Create a DocumentBuilder
            DocumentBuilder builder = factory.newDocumentBuilder();

            // Step 4: Parse the XML file
            File xmlFile = new File("path/to/your/xmlfile.xml");
            Document document = builder.parse(xmlFile);

            // Step 5: Interact with the Document
            document.getDocumentElement().normalize();
            System.out.println("Root element: " + document.getDocumentElement().getNodeName());

            // Further processing of the document...
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

Explanation
Create a DocumentBuilderFactory:
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();

Configure the Factory (optional):
factory.setNamespaceAware(true);
factory.setValidating(false);
factory.setIgnoringElementContentWhitespace(true);

Create a DocumentBuilder:
DocumentBuilder builder = factory.newDocumentBuilder();

Parse the XML Document:
File xmlFile = new File("path/to/your/xmlfile.xml");
Document document = builder.parse(xmlFile);

Interact with the Document:
document.getDocumentElement().normalize();
System.out.println("Root element: " + document.getDocumentElement().getNodeName());


Configurable Features
Namespace Awareness: Set to true to make the parser aware of XML namespaces.
Validation: Set to true to enable XML validation against a DTD or schema.
Whitespace Handling: Configure whether to ignore whitespace in element content.

Using DocumentBuilderFactory and DocumentBuilder is a powerful way to parse and manipulate XML documents in Java, providing a robust API for interacting with XML data.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
DocumentBuilderFactory

Constructor
protected DocumentBuilderFactory()
This is the protected constructor to prevent instantiation.
The line protected DocumentBuilderFactory() indicates that the constructor for the DocumentBuilderFactory class is protected. In Java, a protected constructor means that the constructor can only be accessed within its own package and by subclasses. This restriction prevents direct instantiation of the DocumentBuilderFactory class from outside its package or by classes that are not subclasses.

Explanation
1.Preventing Direct Instantiation: By making the constructor protected, the class ensures that it cannot be directly instantiated using the new keyword by external classes. Instead, the class typically provides a static method to create an instance.
2.Controlled Creation: This approach is often used in factory design patterns to control the creation of instances. For example, a static factory method (newInstance()) is usually provided to create and return instances of the class.

Example with DocumentBuilderFactory
The DocumentBuilderFactory class uses this pattern. You cannot directly create an instance of DocumentBuilderFactory using new DocumentBuilderFactory(). Instead, you use the provided static method newInstance() to get an instance.

code example
public abstract class DocumentBuilderFactory {
    // Protected constructor
    protected DocumentBuilderFactory() {
        // Initialization code
    }

    // Static factory method to get an instance
    public static DocumentBuilderFactory newInstance() {
        // Returns an instance of a concrete subclass
        return new DocumentBuilderFactoryImpl();
    }
    
    // Abstract methods to be implemented by subclasses
    public abstract DocumentBuilder newDocumentBuilder() throws ParserConfigurationException;
}

// Concrete subclass (example)
class DocumentBuilderFactoryImpl extends DocumentBuilderFactory {
    public DocumentBuilderFactoryImpl() {
        super();
    }

    @Override
    public DocumentBuilder newDocumentBuilder() throws ParserConfigurationException {
        return new DocumentBuilderImpl();
    }
}

// DocumentBuilder interface (simplified)
public interface DocumentBuilder {
    Document parse(File file) throws Exception;
}

// Concrete implementation of DocumentBuilder (example)
class DocumentBuilderImpl implements DocumentBuilder {
    @Override
    public Document parse(File file) throws Exception {
        // Parsing logic
        return null;
    }
}

Client Code
public class Main {
    public static void main(String[] args) {
        // Get an instance of DocumentBuilderFactory using the static factory method
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();

        try {
            // Get a DocumentBuilder from the factory
            DocumentBuilder builder = factory.newDocumentBuilder();
            
            // Parse an XML file
            File xmlFile = new File("path/to/your/xmlfile.xml");
            Document document = builder.parse(xmlFile);
            
            // Work with the parsed Document
            System.out.println("Root element: " + document.getDocumentElement().getNodeName());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

Key Points
Protected Constructor: The constructor protected DocumentBuilderFactory() is protected to prevent direct instantiation.
Static Factory Method: The static method newInstance() is provided to get an instance of DocumentBuilderFactory.
Abstract Class: DocumentBuilderFactory is abstract, meaning it cannot be instantiated directly and must be subclassed.
Encapsulation: This design encapsulates the creation logic, providing flexibility and control over how instances are created and managed.
By using a protected constructor and a static factory method, the DocumentBuilderFactory class ensures that instances are created in a controlled manner, promoting good design practices and enhancing code maintainability.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Javax.xml.Parsers.DocumentBuilder Class
DocumentBuilder is a class in the Java API that provides the capability to parse XML documents and build a DOM (Document Object Model) representation of the XML content. It is part of the javax.xml.parsers package, which includes classes for parsing XML documents using the DOM and SAX (Simple API for XML) parsers.

Key Features of DocumentBuilder
1.Parsing XML: DocumentBuilder can parse XML content from various input sources, such as files, input streams, URLs, and SAX input sources.
2.Creating DOM Trees: The primary purpose of DocumentBuilder is to create a DOM tree from an XML document, which can then be manipulated using the DOM API.
3.Validation: DocumentBuilder can be configured to validate the XML content against a DTD (Document Type Definition) or XML Schema during parsing.
4.Namespace Awareness: It can be configured to be aware of XML namespaces, allowing for more precise XML document parsing and handling.

Basic Steps to Use DocumentBuilder
1.Create a DocumentBuilderFactory Instance: Use this factory to configure and obtain a DocumentBuilder instance.
2.Configure the Factory (Optional): Set any desired configuration options on the factory.
3.Create a DocumentBuilder Instance: Obtain the DocumentBuilder from the factory.
4.Parse the XML Document: Use the DocumentBuilder to parse the XML document and obtain a Document object.
5.Manipulate the Document: Interact with the Document object using the DOM API to manipulate the XML content.

Example Usage
Step-by-Step Example
Create and Configure the Factory:
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.DocumentBuilder;
import org.w3c.dom.Document;
import java.io.File;

public class XMLParserExample {
    public static void main(String[] args) {
        try {
            // Step 1: Create a DocumentBuilderFactory
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            
            // Step 2: Configure the factory (optional)
            factory.setNamespaceAware(true);
            factory.setValidating(false);
            factory.setIgnoringElementContentWhitespace(true);

            // Step 3: Create a DocumentBuilder
            DocumentBuilder builder = factory.newDocumentBuilder();

            // Step 4: Parse the XML file
            File xmlFile = new File("path/to/your/xmlfile.xml");
            Document document = builder.parse(xmlFile);

            // Step 5: Interact with the Document
            document.getDocumentElement().normalize();
            System.out.println("Root element: " + document.getDocumentElement().getNodeName());

            // Further processing of the document...

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
Explanation
1.Create a DocumentBuilderFactory:
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();

2.Configure the Factory (Optional):
factory.setNamespaceAware(true);
factory.setValidating(false);
factory.setIgnoringElementContentWhitespace(true);

3.Create a DocumentBuilder:
DocumentBuilder builder = factory.newDocumentBuilder();

4.Parse the XML Document:
File xmlFile = new File("path/to/your/xmlfile.xml");
Document document = builder.parse(xmlFile);

5.Interact with the Document:
document.getDocumentElement().normalize();
System.out.println("Root element: " + document.getDocumentElement().getNodeName());

Configurable Features
* Namespace Awareness: factory.setNamespaceAware(true); allows the parser to understand XML namespaces.
* Validation: factory.setValidating(true); enables validation against a DTD or schema.
* Whitespace Handling: factory.setIgnoringElementContentWhitespace(true); ignores insignificant whitespace in element content.

Key Methods of DocumentBuilder
* parse(File f): Parses the content of the specified file as an XML document.
* parse(InputStream is): Parses the content of the specified input stream as an XML document.
* parse(String uri): Parses the content of the specified URI as an XML document.
* newDocument(): Creates a new DOM Document object, which can be used to build a new XML document.

By using DocumentBuilder, you can easily parse, create, and manipulate XML documents in Java, leveraging the powerful and flexible DOM API.

