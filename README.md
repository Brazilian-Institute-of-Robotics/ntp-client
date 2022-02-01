# Mbed OS NTP Client

This library allows you to fetch time information from a NTP server.

For an example application, please see https://github.com/ARMmbed/ntp-client-example.

## Usage
> **Note:** This library is not intended to be compiled by itself. Therefore, the consumer application must link to it.

To use the library with Mbed OS 6 just add the command below in the application's `CMakeLists.txt` file

```cmake
find_package(mbed_ntp_client REQUIRED CONFIG)
```

and then link with your application, for example

```cmake
[...]

  add_executable(${APP_TARGET}
    src/main.cpp
  )

  target_include_directories(${APP_TARGET}
    PRIVATE  
      include
  )

  target_link_libraries(${APP_TARGET}
    PRIVATE
      mbed-os
      mbed_ntp_client::mbed_ntp_client
  )

[...]
```

## API

### `NTPClient(NetworkInterface *iface)` [constructor]

Create an NTP client. You need to provide a pointer to an [Mbed OS NetworkInterface](https://os.mbed.com/docs/mbed-os/v5.13/apis/network-socket.html). The interface should be connected and ready before calling `get_timestamp`.

### `time_t NTPClient::get_timestamp(int timeout)`

Return time information, typed as a [`time_t`](http://www.cplusplus.com/reference/ctime/time_t/). You can pass in an optional timeout argument (defaults to 15000 milliseconds). For information on timeout values, please see the [Mbed OS Socket documentation](https://os.mbed.com/docs/mbed-os/v5.13/apis/socket.html).

### `void set_server(char* server, int port)`

Change the NTP server and port. The default server is `2.pool.ntp.org` and the default port is `123`.
