# Container MCP Server

This is a simple MCP-based interface for a sandboxed development environment.

## Local dev

Currently a work in progress. Cloudchamber local dev isn't implemented yet, so we are doing a bit of a hack to just run the server in your local environment.

TODO: replace locally running server with the real docker container.

## Deploying

1. Make sure the docker daemon is running

2. Disable WARP and run

```
npx https://prerelease-registry.devprod.cloudflare.dev/workers-sdk/runs/14387504770/npm-package-wrangler-8740 deploy
```

3. Add to your Claude config. If using with Claude, you'll need to disable WARP:

```
{
    "mcpServers": {
        "container": {
            "command": "npx",
            "args": [
                "mcp-remote",
                // this is my deployed instance
                "https://container-starter-2.cmsparks.workers.dev/sse"
            ]
        }
    }
}
```

## Tools

- `container_initialize`: (Re)start a container. Containers are intended to be ephemeral and don't save any state. Containers are only guaranteed to last 10m (this is just because I have a max of like ~5 containers per account).
- `container_ping`: Ping a container for connectivity
- `container_exec`: Run a command in the shell
- `container_files_write`: Write to a file
- `container_files_list`: List all files in the work directory
- `container_file_read`: Read the contents of a single file or directory

## Resources

TODO

Tried implementing these, but MCP clients don't support resources well at all.

## Prompts

TODO

## Container support

The container currently runs python and node. It's connected to the internet and LLMs can install whatever packages.
