env.DIST = 'bionic'
env.TYPE = 'unstable'
env.APTLY_REPOSITORY = 'dev/unstable'
env.PWD_BIND = '/workspace'

node('master') {
    wrap([$class: 'TimestamperBuildWrapper']) {
        wrap([$class: 'AnsiColorBuildWrapper', colorMapName: 'xterm']) {
            stage('clone[code]') {
                checkout scm
            }

            stage('clone[asgen]') {
                sh '[ -d asgen ] || mkdir asgen'
                dir('asgen') {
                    git branch: 'bionic-with-http-fix', url: 'https://github.com/apachelogger/appstream-generator.git'
                }
            }

            stage('generate') {
                sh '~/tooling/nci/contain.rb /workspace/asgen.rb'
                sh 'tree asgen/run/' // Debug
            }

            stage('publish') {
                dir('asgen') {
                    sh '~/tooling/nci/asgen_push.rb'
                    sh 'mkdir -p /var/www/metadata/appstream/$APTLY_REPOSITORY || true'
                    sh 'cp -rv run/export/. /var/www/metadata/appstream/$APTLY_REPOSITORY'
                }
            }
        }
    }
}
