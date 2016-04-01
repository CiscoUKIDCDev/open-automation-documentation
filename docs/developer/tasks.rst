Tasks
=====

To create tasks and make them availbe you will need to create two classes;

* <name>Config.java
* <name>Task.java

The jdo.files will also need to be created/updated.

You will also need to add the task classes to the main module


<name>Config.java
-----------------

dikb::

@PersistenceCapable(detachable = "true", table = "spark_dummy")
public class SparkDummyConfig implements TaskConfigIf {

	public static final String displayLabel = "Spark Get Inventory";
	@Persistent
	private long configEntryId;
	@Persistent
	private long actionId;

	@FormField(label = "Spark Array IP", help = "spark Array IP Address", mandatory = true)
	@UserInputField(type = WorkflowInputFieldTypeDeclaration.IPADDRESS)
	@Persistent
	private String	ipAddress = "";

	@FormField(label = "Spark Username", help = "spark username", mandatory = true, type = FormFieldDefinition.FIELD_TYPE_TEXT)
	@UserInputField(type = SparkConstants.GENERIC_TEXT_INPUT)
	@Persistent
	private String	username;

	@FormField(label = "Password", help = "Password", mandatory = true, type = FormFieldDefinition.FIELD_TYPE_PASSWORD)
	@UserInputField(type = SparkConstants.PASSWORD)
	@Persistent
	private String	password;


<name>Data.java
----------------




jdo.files
----------


Main Module
------------
