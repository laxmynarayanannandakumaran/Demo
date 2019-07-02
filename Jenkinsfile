properties([
    parameters([
        string(name: 'SITE_URL', defaultValue: 'http://a350198f19cb611e9819706be951a32b-1037873391.eu-west-1.elb.amazonaws.com:8090/',
                description: 'URL to test the accesibility against')
    ])
])

SITE_URL = params.SITE_URL ?: 'http://a350198f19cb611e9819706be951a32b-1037873391.eu-west-1.elb.amazonaws.com:8090/'

stage('Test URL') {
    node {
        deleteDir()
        checkout scm

        docker.build('automation/pa11y')
            .inside {
            sh """
                pa11y -c /pa11y.config.json "${SITE_URL}"
            """
        }
    }
}

