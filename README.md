# SSW345 - HW4/REST Lab - Christian Kubelle


## Part 1 & 2 of the REST LAB:

![Screenshot](https://user-images.githubusercontent.com/44238558/112502342-607b4400-8d60-11eb-960e-c4e0fa25ee0d.png)

## Write code for listBranches in a given repo under an owner. See list branches

```javascript
// 1. Write code for listBranches in a given repo under an owner. See list branches
async function listBranches(owner,repo)
{
	let options = getDefaultOptions(`/repos/${owner}/${repo}/branches`, "GET");

	// Send a http request to url and specify a callback that will be called upon its return.
	return new Promise(function(resolve, reject)
	{
		request(options, function (error, response, body) {

			if( error )
			{
				console.log( chalk.red( error ));
				reject(error);
				return; // Terminate execution.
			}

			var obj = JSON.parse(body);
			for( var i = 0; i < obj.length; i++ )
			{
				var name = obj[i].name;
				console.log( name );
			}
			//console.debug( options );
			resolve( JSON.parse(body) );

		});
	});
}
```

## Write code for create a new repo
```javascript
// 2. Write code to create a new repo
async function createRepo(owner,repo)
{
	let options = getDefaultOptions(`/user/repos`, "POST");
	options.json = {
		"name": repo,
		"description": "This is your first repository",
		"homepage": "https://github.com",
		"private": false,
		"has_issues": true,
		"has_projects": true,
		"has_wiki": true
	};

	// Send a http request to url and specify a callback that will be called upon its return.
	return new Promise(function(resolve, reject)
	{
		request(options, function (error, response, body) {


			if( error )
			{
				console.log( chalk.red( error ));
				reject(error);
				return; // Terminate execution.
			}
			resolve( response.statusCode );

		});
	});

}
```
## Write code for creating an issue (Links to an external site.) for an existing repo
```javascript
// 3. Write code for creating an issue for an existing repo.
async function createIssue(owner,repo, issueName, issueBody)
{
	let options = getDefaultOptions(`/repos/${owner}/${repo}/issues`, "POST");
	options.json = {
		title : issueName,
		body : issueBody
	};

	// Send a http request to url and specify a callback that will be called upon its return.
	return new Promise(function(resolve, reject)
	{
		request(options, function (error, response, body) {

			if( error )
			{
				console.log( chalk.red( error ));
				reject(error);
				return; // Terminate execution.
			}

			resolve( response.statusCode );

		});
	});
}
```

## Write code for editing a repo (Links to an external site.) to enable wiki support
```javascript
// 4. Write code for editing a repo to enable wiki support.
async function enableWikiSupport(owner,repo)
{
	let options = getDefaultOptions(`/repos/${owner}/${repo}`, "PATCH");
	options.json = {has_wiki : true}
	// Send a http request to url and specify a callback that will be called upon its return.
	return new Promise(function(resolve, reject)
	{
		request(options, function (error, response, body) {

			if( error )
			{
				console.log( chalk.red( error ));
				reject(error);
				return; // Terminate execution.
			}

			resolve( JSON.parse(JSON.stringify(body)) );
		});
	});	
}
```

## Proof that code is working as intended 
![test](https://github.com/ckubelle/HW4/blob/main/PassedTests.PNG)

## REST Server Portion Video:
[![Screencast](https://user-images.githubusercontent.com/44238558/112762161-434aad80-8fcc-11eb-9e72-47e77f4f241b.png)](https://github.com/ckubelle/HW4/blob/main/Screencast.mp4)

