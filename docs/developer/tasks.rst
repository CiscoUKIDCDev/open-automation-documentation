Tasks
=====

To create tasks and make them availbe you will need to create two classes;

* <name>Config.java
* <name>Task.java

The jdo.files will also need to be created/updated.

You will also need to add the task classes to the main module


<name>Config.java
-----------------

dikb

.. code-block:: java

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



some other text.

<name>Data.java
----------------

.. code-block:: java

    public class SparkDummyTask extends AbstractTask {

    	private static Logger logger = Logger.getLogger( SparkDummyTask.class );

    	@Override
    	public void executeCustomAction(CustomActionTriggerContext context,
    			CustomActionLogger actionLogger) throws Exception {
    		SparkDummyConfig config = (SparkDummyConfig) context.loadConfigObject();

    		String username = config.getUsername();
    		String password = config.getPassword();
    		String ipAddress = config.getIpAddress();

    		String arrayName = "";


    	/* Code */
    	}

    	@Override
    	public TaskConfigIf getTaskConfigImplementation() {
    		return new SparkDummyConfig();
    	}

    	@Override
    	public String getTaskName() {
    		return SparkDummyConfig.displayLabel;
    	}

    	@Override
    	public TaskOutputDefinition[] getTaskOutputDefinitions() {
    		return null;
    	}
    }


jdo.files
----------

.. code-block:: java

    //Each package with config classes should have a file called jdo.files
    //Each config class should be listed in the format below
    //This file informs the build file which classes need to go through JDO enhancement
    +SparkDummyConfig

Main Module
------------

.. code-block:: java

    @Override
    	public AbstractTask[] getTasks() {
    		AbstractTask task1   = new SparkDummyTask();
    		AbstractTask task2   = new SparkMessageCreateTask();

    		AbstractTask[] tasks = new AbstractTask[2];
    		tasks[0]  = task1;
    		tasks[1]  = task2;

    		return tasks;
    	}
