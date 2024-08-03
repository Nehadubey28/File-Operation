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


