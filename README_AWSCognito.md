# AWS Cognito
Below Steps will help to integrate AWS Cognito with Grafana for Users Authentication 


# 1. Install Kube-Prometheus-Stack for Grafana 
Reference Documentation is as below:  

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

This will installs the kube-prometheus stack, a collection of Kubernetes manifests, Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator.

Below Steps needs to be followed: 

    helm upgrade --install grafana prometheus-community/kube-prometheus-stack -n metrics --values grafana-aws-cognito.yaml

# 2. Create sample Grafana application in AWS Cognito for users authentication 

Below Steps needs to be followed: 

    1. Go to Amazon Cognito
    2. Create a userpool
        a. Configure user pool sign-in experience
            Select User Name, Email 
            Allow users to sign in with a preferred user name
            Make user name case sensitive
        b. Configure security requirements
            Select Cognito defaults
            Select No MFA
            Enable self-service account recovery - Recommended
            Email only
        c. Configure sign-up experience
            Enable self-registration
            Allow Cognito to automatically send messages to verify and confirm - Recommended
            Send email message, verify email address
            Required attributes -- > Select Name
        d. Configure message delivery
            Send email with Cognito
        e. Integrate your app
            User pool name -- > aws-grafana-users
            Use the Cognito Hosted UI
            Use a Cognito domain
            Initial app client
            Public Client
            Generate a client secret
            Allowed callback URLs  --- http://localhost:3000/login/generic_oauth
            Add ALLOW_USER_PASSWORD_AUTH and ALLOW_ADMIN_USER_PASSWORD_AUTH to the authentication flows
            Remove the unused Phone number and add OpenID, aws.cognito.signin.user.admin and Profile
            Allowed sign-out URLs - optional -- http://localhost:3000/login/generic_oauth
        f.  Review and create the Pool




