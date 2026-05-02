---
api_specs:
- filename: jupyter-notebook-rest-api-openapi.yml
  format: yaml
  label: Jupyter Notebook REST API
  slug: jupyter-notebook-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/jupyter-notebook/refs/heads/main/openapi/jupyter-notebook-rest-api-openapi.yml
- filename: jupyter-kernel-gateway-api-openapi.yml
  format: yaml
  label: Jupyter Kernel Gateway API
  slug: jupyter-kernel-gateway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/jupyter-notebook/refs/heads/main/openapi/jupyter-kernel-gateway-api-openapi.yml
- filename: jupyterhub-rest-api-openapi.yml
  format: yaml
  label: JupyterHub REST API
  slug: jupyterhub-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/jupyter-notebook/refs/heads/main/openapi/jupyterhub-rest-api-openapi.yml
- filename: jupyter-kernel-messaging-asyncapi.yml
  format: yaml
  label: Jupyter Kernel Messaging Protocol
  slug: jupyter-kernel-messaging
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/jupyter-notebook/refs/heads/main/asyncapi/jupyter-kernel-messaging-asyncapi.yml
channels:
- description: ''
  name: /api/kernels/{kernel_id}/channels
  operation: publish
  operation_id: sendKernelMessage
  summary: Send a message to the kernel
description: The Jupyter Kernel Messaging Protocol defines the WebSocket-based communication between Jupyter clients (notebooks, consoles) and computational kernels. Messages are exchanged over WebSocket channels for shell requests/replies, IOPub broadcasts, stdin input requests, and control channel operations. This protocol is documented in the Jupyter Client messaging specification.
layout: asyncapi
messages:
- description: ''
  name: ExecuteRequest
  summary: Request to execute code in the kernel.
  title: Execute Request
- description: ''
  name: ExecuteReply
  summary: Reply to an execute request with status and execution count.
  title: Execute Reply
- description: ''
  name: InspectRequest
  summary: Request to inspect an object at cursor position.
  title: Inspect Request
- description: ''
  name: InspectReply
  summary: Reply with object inspection results.
  title: Inspect Reply
- description: ''
  name: CompleteRequest
  summary: Request code completion suggestions.
  title: Complete Request
- description: ''
  name: CompleteReply
  summary: Reply with code completion matches.
  title: Complete Reply
- description: ''
  name: HistoryRequest
  summary: Request execution history from the kernel.
  title: History Request
- description: ''
  name: HistoryReply
  summary: Reply with execution history entries.
  title: History Reply
- description: ''
  name: IsCompleteRequest
  summary: Check if code is complete and ready to execute.
  title: Is Complete Request
- description: ''
  name: IsCompleteReply
  summary: Reply indicating whether code is complete.
  title: Is Complete Reply
- description: ''
  name: KernelInfoRequest
  summary: Request information about the kernel.
  title: Kernel Info Request
- description: ''
  name: KernelInfoReply
  summary: Reply with kernel implementation and language information.
  title: Kernel Info Reply
- description: ''
  name: ShutdownRequest
  summary: Request the kernel to shut down.
  title: Shutdown Request
- description: ''
  name: ShutdownReply
  summary: Reply confirming kernel shutdown.
  title: Shutdown Reply
- description: ''
  name: InterruptRequest
  summary: Request to interrupt the kernel.
  title: Interrupt Request
- description: ''
  name: InputRequest
  summary: Kernel requests input from the frontend (e.g., for Python's input() function).
  title: Input Request
- description: ''
  name: InputReply
  summary: Frontend sends user input to the kernel.
  title: Input Reply
- description: ''
  name: ExecuteInput
  summary: Broadcast of code being executed (for all connected clients).
  title: Execute Input Broadcast
- description: ''
  name: ExecuteResult
  summary: Result of an execution, equivalent to the Out[] prompt in IPython. Contains rich display data.
  title: Execute Result
- description: ''
  name: StreamOutput
  summary: Standard output or standard error stream data from code execution.
  title: Stream Output
- description: ''
  name: DisplayData
  summary: Rich display data output from code execution, supporting multiple MIME types.
  title: Display Data
- description: ''
  name: UpdateDisplayData
  summary: Update a previous display_data output.
  title: Update Display Data
- description: ''
  name: ErrorOutput
  summary: Error output from failed code execution.
  title: Error Output
- description: ''
  name: StatusBroadcast
  summary: Kernel execution state broadcast. Published on every state change (busy, idle, starting).
  title: Kernel Status
- description: ''
  name: ClearOutput
  summary: Request to clear output area in the frontend.
  title: Clear Output
- description: ''
  name: CommOpen
  summary: Open a comm channel for custom messaging (e.g., widgets).
  title: Comm Open
- description: ''
  name: CommMsg
  summary: Send a message on an open comm channel.
  title: Comm Message
- description: ''
  name: CommClose
  summary: Close a comm channel.
  title: Comm Close
- description: ''
  name: CommOpenReply
  summary: Kernel opens a comm channel to the frontend.
  title: Comm Open (from kernel)
- description: ''
  name: CommMsgReply
  summary: Kernel sends a message on an open comm channel.
  title: Comm Message (from kernel)
- description: ''
  name: CommCloseReply
  summary: Kernel closes a comm channel.
  title: Comm Close (from kernel)
- description: ''
  name: DebugReply
  summary: Reply to a debug request.
  title: Debug Reply
- description: ''
  name: DebugEvent
  summary: Debug event broadcast from the kernel.
  title: Debug Event
name: Jupyter Kernel Messaging Protocol
provider_name: Jupyter Notebook
provider_slug: jupyter-notebook
servers:
- description: WebSocket endpoint for communicating with a running Jupyter kernel. All messaging channels (shell, iopub, stdin, control) are multiplexed over this single WebSocket connection.
  name: local
  protocol: ws
  url: ws://localhost:8888/api/kernels/{kernel_id}/channels
slug: jupyter-kernel-messaging-asyncapi
source_filename: jupyter-kernel-messaging-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Jupyter Kernel Messaging Protocol\n  version: 5.4.0\n  description: >-\n    The Jupyter Kernel Messaging Protocol defines the WebSocket-based\n    communication between Jupyter clients (notebooks, consoles) and\n    computational kernels. Messages are exchanged over WebSocket\n    channels for shell requests/replies, IOPub broadcasts, stdin\n    input requests, and control channel operations. This protocol\n    is documented in the Jupyter Client messaging specification.\n  license:\n    name: BSD-3-Clause\n    url: https://opensource.org/licenses/BSD-3-Clause\n  contact:\n    name: Jupyter Project\n    url: https://jupyter-client.readthedocs.io/en/stable/messaging.html\n    email: jupyter@googlegroups.com\nservers:\n  local:\n    url: ws://localhost:8888/api/kernels/{kernel_id}/channels\n    protocol: ws\n    description: >-\n      WebSocket endpoint for communicating with a running Jupyter\n      kernel. All messaging channels (shell, iopub,\
  \ stdin, control)\n      are multiplexed over this single WebSocket connection.\nchannels:\n  /api/kernels/{kernel_id}/channels:\n    parameters:\n      kernel_id:\n        description: The unique identifier of the kernel.\n        schema:\n          type: string\n          format: uuid\n    publish:\n      operationId: sendKernelMessage\n      summary: Send a message to the kernel\n      description: >-\n        Send a message to the kernel on the shell, stdin, or control\n        channel. The channel is indicated by the channel field in the\n        message wrapper.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ExecuteRequest'\n          - $ref: '#/components/messages/InspectRequest'\n          - $ref: '#/components/messages/CompleteRequest'\n          - $ref: '#/components/messages/HistoryRequest'\n          - $ref: '#/components/messages/IsCompleteRequest'\n          - $ref: '#/components/messages/KernelInfoRequest'\n          - $ref: '#/components/messages/ShutdownRequest'\n\
  \          - $ref: '#/components/messages/InterruptRequest'\n          - $ref: '#/components/messages/InputReply'\n          - $ref: '#/components/messages/CommOpen'\n          - $ref: '#/components/messages/CommMsg'\n          - $ref: '#/components/messages/CommClose'\n    subscribe:\n      operationId: receiveKernelMessage\n      summary: Receive a message from the kernel\n      description: >-\n        Receive messages from the kernel on the shell (reply), iopub\n        (broadcast), or stdin channel.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ExecuteReply'\n          - $ref: '#/components/messages/InspectReply'\n          - $ref: '#/components/messages/CompleteReply'\n          - $ref: '#/components/messages/HistoryReply'\n          - $ref: '#/components/messages/IsCompleteReply'\n          - $ref: '#/components/messages/KernelInfoReply'\n          - $ref: '#/components/messages/ShutdownReply'\n          - $ref: '#/components/messages/ExecuteInput'\n\
  \          - $ref: '#/components/messages/ExecuteResult'\n          - $ref: '#/components/messages/StreamOutput'\n          - $ref: '#/components/messages/DisplayData'\n          - $ref: '#/components/messages/UpdateDisplayData'\n          - $ref: '#/components/messages/ErrorOutput'\n          - $ref: '#/components/messages/StatusBroadcast'\n          - $ref: '#/components/messages/ClearOutput'\n          - $ref: '#/components/messages/InputRequest'\n          - $ref: '#/components/messages/CommOpenReply'\n          - $ref: '#/components/messages/CommMsgReply'\n          - $ref: '#/components/messages/CommCloseReply'\n          - $ref: '#/components/messages/DebugReply'\n          - $ref: '#/components/messages/DebugEvent'\ncomponents:\n  messages:\n    ExecuteRequest:\n      name: execute_request\n      title: Execute Request\n      summary: Request to execute code in the kernel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n\
  \      x-channel: shell\n      headers:\n        type: object\n        properties:\n          msg_type:\n            type: string\n            const: execute_request\n    ExecuteReply:\n      name: execute_reply\n      title: Execute Reply\n      summary: Reply to an execute request with status and execution count.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    InspectRequest:\n      name: inspect_request\n      title: Inspect Request\n      summary: Request to inspect an object at cursor position.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    InspectReply:\n      name: inspect_reply\n      title: Inspect Reply\n      summary: Reply with object inspection results.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    CompleteRequest:\n\
  \      name: complete_request\n      title: Complete Request\n      summary: Request code completion suggestions.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    CompleteReply:\n      name: complete_reply\n      title: Complete Reply\n      summary: Reply with code completion matches.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    HistoryRequest:\n      name: history_request\n      title: History Request\n      summary: Request execution history from the kernel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    HistoryReply:\n      name: history_reply\n      title: History Reply\n      summary: Reply with execution history entries.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n\
  \      x-channel: shell\n    IsCompleteRequest:\n      name: is_complete_request\n      title: Is Complete Request\n      summary: Check if code is complete and ready to execute.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    IsCompleteReply:\n      name: is_complete_reply\n      title: Is Complete Reply\n      summary: Reply indicating whether code is complete.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    KernelInfoRequest:\n      name: kernel_info_request\n      title: Kernel Info Request\n      summary: Request information about the kernel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    KernelInfoReply:\n      name: kernel_info_reply\n      title: Kernel Info Reply\n      summary: Reply with kernel implementation and language\
  \ information.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    ShutdownRequest:\n      name: shutdown_request\n      title: Shutdown Request\n      summary: Request the kernel to shut down.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: control\n    ShutdownReply:\n      name: shutdown_reply\n      title: Shutdown Reply\n      summary: Reply confirming kernel shutdown.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: control\n    InterruptRequest:\n      name: interrupt_request\n      title: Interrupt Request\n      summary: Request to interrupt the kernel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: control\n    InputRequest:\n      name: input_request\n      title: Input Request\n\
  \      summary: >-\n        Kernel requests input from the frontend (e.g., for Python's\n        input() function).\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: stdin\n    InputReply:\n      name: input_reply\n      title: Input Reply\n      summary: Frontend sends user input to the kernel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: stdin\n    ExecuteInput:\n      name: execute_input\n      title: Execute Input Broadcast\n      summary: Broadcast of code being executed (for all connected clients).\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    ExecuteResult:\n      name: execute_result\n      title: Execute Result\n      summary: >-\n        Result of an execution, equivalent to the Out[] prompt in\n        IPython. Contains rich display data.\n\
  \      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    StreamOutput:\n      name: stream\n      title: Stream Output\n      summary: >-\n        Standard output or standard error stream data from\n        code execution.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    DisplayData:\n      name: display_data\n      title: Display Data\n      summary: >-\n        Rich display data output from code execution, supporting\n        multiple MIME types.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    UpdateDisplayData:\n      name: update_display_data\n      title: Update Display Data\n      summary: Update a previous display_data output.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n   \
  \   x-channel: iopub\n    ErrorOutput:\n      name: error\n      title: Error Output\n      summary: Error output from failed code execution.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    StatusBroadcast:\n      name: status\n      title: Kernel Status\n      summary: >-\n        Kernel execution state broadcast. Published on every state\n        change (busy, idle, starting).\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    ClearOutput:\n      name: clear_output\n      title: Clear Output\n      summary: Request to clear output area in the frontend.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    CommOpen:\n      name: comm_open\n      title: Comm Open\n      summary: Open a comm channel for custom messaging (e.g., widgets).\n   \
  \   contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    CommMsg:\n      name: comm_msg\n      title: Comm Message\n      summary: Send a message on an open comm channel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    CommClose:\n      name: comm_close\n      title: Comm Close\n      summary: Close a comm channel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: shell\n    CommOpenReply:\n      name: comm_open\n      title: Comm Open (from kernel)\n      summary: Kernel opens a comm channel to the frontend.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    CommMsgReply:\n      name: comm_msg\n      title: Comm Message (from kernel)\n      summary: Kernel sends a message on\
  \ an open comm channel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    CommCloseReply:\n      name: comm_close\n      title: Comm Close (from kernel)\n      summary: Kernel closes a comm channel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n    DebugReply:\n      name: debug_reply\n      title: Debug Reply\n      summary: Reply to a debug request.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: control\n    DebugEvent:\n      name: debug_event\n      title: Debug Event\n      summary: Debug event broadcast from the kernel.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KernelMessage'\n      x-channel: iopub\n  schemas:\n    KernelMessage:\n      type: object\n      description: >-\n        A Jupyter kernel\
  \ message envelope. All messages follow this\n        structure with a header, parent_header, metadata, content,\n        and optional buffers.\n      properties:\n        header:\n          $ref: '#/components/schemas/MessageHeader'\n        parent_header:\n          description: >-\n            Header of the message this is a reply to. Empty object\n            for initial requests.\n          oneOf:\n            - $ref: '#/components/schemas/MessageHeader'\n            - type: object\n        metadata:\n          type: object\n          description: Message metadata.\n          additionalProperties: true\n        content:\n          description: >-\n            The message content. Structure depends on the msg_type.\n          oneOf:\n            - $ref: '#/components/schemas/ExecuteRequestContent'\n            - $ref: '#/components/schemas/ExecuteReplyContent'\n            - $ref: '#/components/schemas/InspectRequestContent'\n            - $ref: '#/components/schemas/InspectReplyContent'\n\
  \            - $ref: '#/components/schemas/CompleteRequestContent'\n            - $ref: '#/components/schemas/CompleteReplyContent'\n            - $ref: '#/components/schemas/HistoryRequestContent'\n            - $ref: '#/components/schemas/HistoryReplyContent'\n            - $ref: '#/components/schemas/IsCompleteRequestContent'\n            - $ref: '#/components/schemas/IsCompleteReplyContent'\n            - $ref: '#/components/schemas/KernelInfoReplyContent'\n            - $ref: '#/components/schemas/ShutdownContent'\n            - $ref: '#/components/schemas/InputRequestContent'\n            - $ref: '#/components/schemas/InputReplyContent'\n            - $ref: '#/components/schemas/StreamContent'\n            - $ref: '#/components/schemas/DisplayDataContent'\n            - $ref: '#/components/schemas/ExecuteResultContent'\n            - $ref: '#/components/schemas/ErrorContent'\n            - $ref: '#/components/schemas/StatusContent'\n            - $ref: '#/components/schemas/ClearOutputContent'\n\
  \            - $ref: '#/components/schemas/CommOpenContent'\n            - $ref: '#/components/schemas/CommMsgContent'\n            - $ref: '#/components/schemas/CommCloseContent'\n        buffers:\n          type: array\n          description: Optional binary buffers (e.g., for comm messages).\n          items:\n            type: string\n            format: byte\n        channel:\n          type: string\n          description: >-\n            The channel this message belongs to when multiplexed\n            over a single WebSocket connection.\n          enum:\n            - shell\n            - iopub\n            - stdin\n            - control\n      required:\n        - header\n        - parent_header\n        - metadata\n        - content\n    MessageHeader:\n      type: object\n      description: Header for a Jupyter kernel message.\n      properties:\n        msg_id:\n          type: string\n          description: Unique message identifier.\n        msg_type:\n          type: string\n\
  \          description: >-\n            The type of message (e.g., execute_request,\n            execute_reply, stream, status).\n        username:\n          type: string\n          description: Username of the message sender.\n        session:\n          type: string\n          description: Session identifier.\n        date:\n          type: string\n          format: date-time\n          description: Timestamp when the message was created.\n        version:\n          type: string\n          description: Message protocol version.\n          default: '5.4'\n      required:\n        - msg_id\n        - msg_type\n        - username\n        - session\n        - date\n        - version\n    ExecuteRequestContent:\n      type: object\n      description: Content for an execute_request message.\n      properties:\n        code:\n          type: string\n          description: The code to execute.\n        silent:\n          type: boolean\n          description: >-\n            If true, signals\
  \ the kernel to execute quietly and\n            not broadcast on IOPub.\n          default: false\n        store_history:\n          type: boolean\n          description: Whether to store this execution in history.\n          default: true\n        user_expressions:\n          type: object\n          description: >-\n            Mapping of names to expressions to evaluate after\n            the code executes.\n          additionalProperties:\n            type: string\n        allow_stdin:\n          type: boolean\n          description: Whether the frontend can provide stdin.\n          default: true\n        stop_on_error:\n          type: boolean\n          description: >-\n            Whether to abort remaining execution queue on error.\n          default: true\n      required:\n        - code\n    ExecuteReplyContent:\n      type: object\n      description: Content for an execute_reply message.\n      properties:\n        status:\n          type: string\n          description: Status\
  \ of the execution.\n          enum:\n            - ok\n            - error\n            - aborted\n        execution_count:\n          type: integer\n          description: The global execution count.\n        user_expressions:\n          type: object\n          description: Results of user_expressions evaluation.\n          additionalProperties: true\n        payload:\n          type: array\n          description: Deprecated payload for page, set_next_input, etc.\n          items:\n            type: object\n            additionalProperties: true\n        traceback:\n          type: array\n          description: Traceback frames if status is error.\n          items:\n            type: string\n        ename:\n          type: string\n          description: Exception name if status is error.\n        evalue:\n          type: string\n          description: Exception value if status is error.\n      required:\n        - status\n        - execution_count\n    InspectRequestContent:\n      type:\
  \ object\n      description: Content for an inspect_request message.\n      properties:\n        code:\n          type: string\n          description: The code context for inspection.\n        cursor_pos:\n          type: integer\n          description: Cursor position within the code.\n        detail_level:\n          type: integer\n          description: >-\n            Level of detail (0 for minimal, 1 for full).\n          enum:\n            - 0\n            - 1\n          default: 0\n      required:\n        - code\n        - cursor_pos\n    InspectReplyContent:\n      type: object\n      description: Content for an inspect_reply message.\n      properties:\n        status:\n          type: string\n          enum:\n            - ok\n            - error\n        found:\n          type: boolean\n          description: Whether an object was found at the cursor position.\n        data:\n          type: object\n          description: MIME-type keyed dictionary of inspection results.\n\
  \          additionalProperties: true\n        metadata:\n          type: object\n          additionalProperties: true\n      required:\n        - status\n        - found\n    CompleteRequestContent:\n      type: object\n      description: Content for a complete_request message.\n      properties:\n        code:\n          type: string\n          description: The code to complete.\n        cursor_pos:\n          type: integer\n          description: Cursor position in the code.\n      required:\n        - code\n        - cursor_pos\n    CompleteReplyContent:\n      type: object\n      description: Content for a complete_reply message.\n      properties:\n        status:\n          type: string\n          enum:\n            - ok\n            - error\n        matches:\n          type: array\n          description: List of completion matches.\n          items:\n            type: string\n        cursor_start:\n          type: integer\n          description: Start of the range to replace with\
  \ completion.\n        cursor_end:\n          type: integer\n          description: End of the range to replace with completion.\n        metadata:\n          type: object\n          additionalProperties: true\n      required:\n        - status\n        - matches\n        - cursor_start\n        - cursor_end\n    HistoryRequestContent:\n      type: object\n      description: Content for a history_request message.\n      properties:\n        output:\n          type: boolean\n          description: Whether to include output.\n          default: false\n        raw:\n          type: boolean\n          description: Whether to return raw input.\n          default: true\n        hist_access_type:\n          type: string\n          description: Type of history access.\n          enum:\n            - range\n            - tail\n            - search\n        session:\n          type: integer\n          description: Session number for range access.\n        start:\n          type: integer\n      \
  \    description: Start index for range access.\n        stop:\n          type: integer\n          description: Stop index for range access.\n        n:\n          type: integer\n          description: Number of entries for tail access.\n        pattern:\n          type: string\n          description: Pattern for search access.\n        unique:\n          type: boolean\n          description: Whether to return only unique entries.\n          default: false\n      required:\n        - output\n        - raw\n        - hist_access_type\n    HistoryReplyContent:\n      type: object\n      description: Content for a history_reply message.\n      properties:\n        status:\n          type: string\n          enum:\n            - ok\n            - error\n        history:\n          type: array\n          description: >-\n            List of history entries as [session, line_number,\n            input] or [session, line_number, [input, output]].\n          items:\n            type: array\n  \
  \    required:\n        - status\n        - history\n    IsCompleteRequestContent:\n      type: object\n      description: Content for an is_complete_request message.\n      properties:\n        code:\n          type: string\n          description: The code to check for completeness.\n      required:\n        - code\n    IsCompleteReplyContent:\n      type: object\n      description: Content for an is_complete_reply message.\n      properties:\n        status:\n          type: string\n          description: Completeness status of the code.\n          enum:\n            - complete\n            - incomplete\n            - invalid\n            - unknown\n        indent:\n          type: string\n          description: >-\n            Indent string to use if status is incomplete.\n      required:\n        - status\n    KernelInfoReplyContent:\n      type: object\n      description: Content for a kernel_info_reply message.\n      properties:\n        status:\n          type: string\n       \
  \   enum:\n            - ok\n            - error\n        protocol_version:\n          type: string\n          description: Messaging protocol version.\n        implementation:\n          type: string\n          description: Kernel implementation name (e.g., ipython).\n        implementation_version:\n          type: string\n          description: Kernel implementation version.\n        language_info:\n          type: object\n          description: Information about the language the kernel executes.\n          properties:\n            name:\n              type: string\n              description: Language name (e.g., python).\n            version:\n              type: string\n              description: Language version.\n            mimetype:\n              type: string\n              description: MIME type for the language.\n            file_extension:\n              type: string\n              description: File extension for the language.\n            pygments_lexer:\n              type:\
  \ string\n              description: Pygments lexer name.\n            codemirror_mode:\n              description: CodeMirror mode specification.\n            nbconvert_exporter:\n              type: string\n              description: nbconvert exporter name.\n          required:\n            - name\n            - version\n            - mimetype\n            - file_extension\n        banner:\n          type: string\n          description: Banner text shown on kernel startup.\n        debugger:\n          type: boolean\n          description: Whether the kernel supports debugging.\n        help_links:\n          type: array\n          description: List of help links.\n          items:\n            type: object\n            properties:\n              text:\n                type: string\n              url:\n                type: string\n                format: uri\n      required:\n        - status\n        - protocol_version\n        - implementation\n        - implementation_version\n\
  \        - language_info\n        - banner\n    ShutdownContent:\n      type: object\n      description: Content for shutdown_request and shutdown_reply messages.\n      properties:\n        restart:\n          type: boolean\n          description: Whether to restart the kernel after shutdown.\n      required:\n        - restart\n    InputRequestContent:\n      type: object\n      description: Content for an input_request message.\n      properties:\n        prompt:\n          type: string\n          description: Prompt text for the user.\n        password:\n          type: boolean\n          description: Whether the input should be hidden (password).\n          default: false\n      required:\n        - prompt\n        - password\n    InputReplyContent:\n      type: object\n      description: Content for an input_reply message.\n      properties:\n        value:\n          type: string\n          description: The user's input value.\n      required:\n        - value\n    StreamContent:\n\
  \      type: object\n      description: Content for a stream message (stdout/stderr).\n      properties:\n        name:\n          type: string\n          description: Stream name.\n          enum:\n            - stdout\n            - stderr\n        text:\n          type: string\n          description: The stream text output.\n      required:\n        - name\n        - text\n    DisplayDataContent:\n      type: object\n      description: Content for display_data and update_display_data messages.\n      properties:\n        data:\n          type: object\n          description: >-\n            MIME-type keyed dictionary of display data\n            (e.g., text/plain, text/html, image/png).\n          additionalProperties: true\n        metadata:\n          type: object\n          description: MIME-type keyed metadata for the display data.\n          additionalProperties: true\n        transient:\n          type: object\n          description: >-\n            Transient data not persisted\
  \ (e.g., display_id).\n          properties:\n            display_id:\n              type: string\n              description: Display identifier for updating.\n      required:\n        - data\n        - metadata\n    ExecuteResultContent:\n      type: object\n      description: Content for an execute_result message.\n      properties:\n        execution_count:\n          type: integer\n          description: The execution count (Out[] number).\n        data:\n          type: object\n          description: MIME-type keyed result data.\n          additionalProperties: true\n        metadata:\n          type: object\n          description: MIME-type keyed metadata.\n          additionalProperties: true\n      required:\n        - execution_count\n        - data\n        - metadata\n    ErrorContent:\n      type: object\n      description: Content for an error message.\n      properties:\n        ename:\n          type: string\n          description: Exception name.\n        evalue:\n    \
  \      type: string\n          description: Exception value.\n        traceback:\n          type: array\n          description: Traceback frames as strings.\n          items:\n            type: string\n      required:\n        - ename\n        - evalue\n        - traceback\n    StatusContent:\n      type: object\n      description: Content for a status message.\n      properties:\n        execution_state:\n          type: string\n          description: Current kernel execution state.\n          enum:\n            - busy\n            - idle\n            - starting\n      required:\n        - execution_state\n    ClearOutputContent:\n      type: object\n      description: Content for a clear_output message.\n      properties:\n        wait:\n          type: boolean\n          description: >-\n            Whether to wait for the next display before clearing.\n      required:\n        - wait\n    CommOpenContent:\n      type: object\n      description: Content for a comm_open message.\n  \
  \    properties:\n        comm_id:\n          type: string\n          description: Unique comm identifier.\n        target_name:\n          type: string\n          description: >-\n            Target name for the comm (e.g., jupyter.widget for\n            ipywidgets).\n        data:\n          type: object\n          description: Initial data for the comm.\n          additionalProperties: true\n      required:\n        - comm_id\n        - target_name\n    CommMsgContent:\n      type: object\n      description: Content for a comm_msg message.\n      properties:\n        comm_id:\n          type: string\n          description: Comm identifier.\n        data:\n          type: object\n          description: Message data.\n          additionalProperties: true\n      required:\n        - comm_id\n        - data\n    CommCloseContent:\n      type: object\n      description: Content for a comm_close message.\n      properties:\n        comm_id:\n          type: string\n          description:\
  \ Comm identifier to close.\n        data:\n          type: object\n          description: Optional closing data.\n          additionalProperties: true\n      required:\n        - comm_id\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/jupyter-notebook/refs/heads/main/asyncapi/jupyter-kernel-messaging-asyncapi.yml
spec_file: asyncapi/jupyter-kernel-messaging-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/jupyter-notebook/refs/heads/main/asyncapi/jupyter-kernel-messaging-asyncapi.yml
tags:
- Data Science
- Interactive Computing
- Jupyter
- Machine Learning
- Notebooks
- Python
- AsyncAPI
- Webhooks
- Events
version: 5.4.0
---
