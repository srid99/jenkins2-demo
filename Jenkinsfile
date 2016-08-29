properties([[$class: 'ParametersDefinitionProperty',
    parameterDefinitions: [
        [$class: 'BooleanParameterDefinition',
         defaultValue: false,
         name: 'BUILD_APP'
        ]
    ]
]])

node {
    checkout scm

    if(${BUILD_APP}) {
       stage 'Build'
       echo 'Build the app'
    }
    
    stage 'Deploy to Test'
    echo 'Deploy the app in Test environment'

    stage 'Test'
    echo 'Test the app'

    if (env.BRANCH_NAME == 'master') {
	stage 'Release'
	echo 'Release the app'

	stage 'Publish artifact'
	echo 'Publish the released version to a artifact repository'

	stage 'Deploy to Prod'
	echo 'All is well. Let\'s push it to Prod'
    }
}

