### This GitHub action is a clone from the exclellent [estherk0/jenkins-trigger](https://github.com/estherk0/jenkins-trigger)
<br />
My reasons for cloning the main repo is that calling:

```javascript
  method: 'POST',
  url: `${jenkinsEndpoint}/job/${jobName}/buildWithParameters`,
```

**does not** always triggers the Jenkins job
<br />
while calling:

```javascript
  method: 'POST',
  url: `${jenkinsEndpoint}/job/${jobName}/build?delay=0sec`,
```

**does** always triggers the Jenkins job.

I'm thinking about making a PR to the main repo
<br />
but at this point, I'm uncertain if the chage will be helpful for all user-cases.
<br />
So I have decided to just make a clone of the original repo that serves my needs :)

-----------------



# Jenkins job trigger action
Github Action to trigger jenkins job and wait for job completion using Jenkins API.  
Welcome your feedback and request. :open_hands:

## Usage
### Generate API token for Jenkins API
Please see [How to get the API Token for Jenkins](https://stackoverflow.com/questions/45466090/how-to-get-the-api-token-for-jenkins)
> 1. Log in Jenkins.
> 2. Click you name (upper-right corner).
> 3. Click Configure (left-side menu).
> 4. Use "Add new Token" button to generate a new one then name it.
> 5. You must copy the token when you generate it as you cannot view the token afterwards.
> 6. Revoke old tokens when no longer needed. 
### Inputs
| name | required | description |
| ---- | -------- | ----------- |
| url  | `true`   | Jenkins full URL including http/https protocol |
| user_name | `true` | User name of Jenkins |
| api_token | `true` | Jenkins API token |
| job_name | `true` | Jenkins job name |
| parameter | false | Job parameter in JSON format. ex) {"param1":"value1"} |
| wait | false | Set true as default. Waiting for job completion or not |
| timeout | false | Set 600 seconds as default. Timeout (seconds) for github action. |

### Example
```yaml
- name: Trigger jenkins job
  uses: IvanDimanov-MoveDigital/jenkins-trigger@main
  with:
    url: ${{ secrets.JENKINS_URL }}
    job_name: "build_web_application"
    user_name: ${{ secrets.JENKINS_USER }}
    api_token: ${{ secrets.JENKINS_TOKEN }}
    wait: "true"
    timeout: "1000"
```
