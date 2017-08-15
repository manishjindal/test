
import hudson.console.*
import hudson.model.*
import groovy.json.JsonSlurper;
import hudson.FilePath


println "Running BranchAction.dsl"

def action = params['Action']	// branch action (Create/Delete)
def source = params['Source']	// source branch (required for Create)
def projects = params['Projects']
def branch = params['Branch']	// branch to create or delete
def archive = params['Archive']	// true/false tag branch before deleting
def desc = params['Description']

def fail(msg) {
	println msg
	build.setResult(Result.FAILURE)
}

if (!(action in ['Create','Delete'])) {
	println "Unrecognized branch action '$action'"
	return false
}

if (action == 'Create' && !desc) {
	fail ("Please provide a short Description for the new Branch")
	return
}

if (!source) {
	if (action == 'Create') {
		println "Branch creation requires a Source branch"
		return false
	} else {
		source = 'N/A'
	}
}
if (!branch) {
	println "Branch name must be provided"
	return false
}
if (action == 'Delete' && branch in ['integration','master']) {
	println "No! I refuse to delete ${branch}! Why would you ask me to do this?"
	return false
}