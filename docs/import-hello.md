
### `import hello from github`
```bash
#!/#!/usr/bin/env import
bin/bash
set -euo pipefail

# `import` debug logs are always enabled during build
export IMPORT_DEBUG=1
export IMPORT_CURL_OPTS="-s -H"
export IMPORT_RELOAD=0

IMPORT_LIB="$IMPORT_CACHE/bin/lib"
lastcmd="| last cmd = $? |" 

handler() {
    echo "Installing static \`package\` binary to \"$IMPORT_LIB\"" \
    eval "$(curl -sfLS \"https://github.com/servingtokens-com/st-import/blob/main/docs/hello.sh\" > $IMPORT_LIB)" \
    echo "$lastcmd" \
    eval "$(. "$IMPORT_LIB/lib")" \
    echo "$lastcmd" \
    echo "listing the contents of the IMPORT_LIB dir" \
    echo "$(ls -laiR $IMPORT_CACHE/bin)" \
    echo "$lastcmd" \
    echo "listing the contents of the IMPORT_LIB dir"
}
```
