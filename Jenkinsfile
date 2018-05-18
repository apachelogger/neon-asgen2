env.DIST = 'bionic'
env.TYPE = 'unstable'
env.APTLY_REPOSITORY = 'dev/unstable'
env.PWD_BIND = '/workspace'

node('master') {
    wrap([$class: 'TimestamperBuildWrapper']) {
        wrap([$class: 'AnsiColorBuildWrapper', colorMapName: 'xterm']) {

            stage 'Clone'
            checkout scm

            stage 'Process'
            sh '~/tooling/nci/contain.rb /workspace/asgen.rb'

            // stage 'Publish'
            // sh '~/tooling/nci/asgen_push.rb'
            // sh 'mkdir -p /var/www/metadata/appstream/$APTLY_REPOSITORY || true'
            // sh 'cp -rv run/export/. /var/www/metadata/appstream/$APTLY_REPOSITORY'
            //
            // stage 'Cleanup'
            // sh '#rm -rf aptly-repository'
        }
    }
}
