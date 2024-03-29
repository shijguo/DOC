											阿里云API

void *IOT_MQTT_Construct(iotx_mqtt_param_t *pInitParams)					//与云端建立MQTT连接, 入参pInitParams为NULL时将会使用默认参数建连。
	pInitParams	MQTT初始化参数,填写NULL将以默认参数建连

	typedef struct {
	    uint16_t                   port;
	    const char                 *host;
	    const char                 *client_id;
	    const char                 *username;
	    const char                 *password;
	    const char                 *pub_key;
	    const char                 *customize_info;
	    uint8_t                    clean_session;
	    uint32_t                   request_timeout_ms;
	    uint32_t                   keepalive_interval_ms;
	    uint32_t                   write_buf_size;
	    uint32_t                   read_buf_size;
	    iotx_mqtt_event_handle_t    handle_event;
	} iotx_mqtt_param_t, *iotx_mqtt_param_pt;

	port: 云端服务器端口
	host: 云端服务器地址
	client_id: MQTT客户端ID
	username: 登录MQTT服务器用户名
	password: 登录MQTT服务器密码
	pub_key: MQTT连接加密方式及密钥
	clean_session: 选择是否使用MQTT协议的clean session特性
	request_timeout_ms: MQTT消息发送的超时时间
	keepalive_interval_ms: MQTT心跳超时时间
	write_buf_size: MQTT消息发送buffer最大长度
	read_buf_size: MQTT消息接收buffer最大长度
	handle_event: 用户回调函数, 用与接收MQTT模块的事件信息
	customize_info: 用户自定义上报信息，是以逗号为分隔符kv字符串，如用户的厂商信息，模组信息自定义字符串为"pid=123456,mid=abcd";



int IOT_MQTT_Destroy(void **phandle)							//销毁指定MQTT连接并释放资源
	phandle		MQTT句柄,可为NULL

int IOT_MQTT_Yield(void *handle, int timeout_ms)					//用于接收网络报文并将消息分发到用户的回调函数中
	handle		MQTT句柄,可为NULL
	timeout_ms	尝试接收报文的超时时间


int IOT_MQTT_CheckStateNormal(void *handle)						//获取当前MQTT连接状态
	handle		MQTT句柄,可为NULL



int IOT_MQTT_Subscribe(void *handle,
                        const char *topic_filter,
                        iotx_mqtt_qos_t qos,
                        iotx_mqtt_event_handle_func_fpt topic_handle_func,
                        void *pcontext)							//向云端订阅指定的MQTT Topic
	handle			MQTT句柄,可为NULL
	topic_filter		需要订阅的topic
	qos			采用的QoS策略
	topic_handle_func	用于接收MQTT消息的回调函数
	pcontext		用户Context, 会通过回调函数送回


IOT_MQTT_Subscribe_Sync(void *handle,
                            const char *topic_filter,
                            iotx_mqtt_qos_t qos,
                            iotx_mqtt_event_handle_func_fpt topic_handle_func,
                            void *pcontext,
                            int timeout_ms);						//向云端订阅指定的MQTT Topic, 该接口为同步接口

	handle			MQTT句柄,可为NULL
	topic_filter		需要订阅的topic
	qos			采用的QoS策略
	topic_handle_func	用于接收MQTT消息的回调函数
	pcontext		用户Context, 会通过回调函数送回
	timeout_ms		该同步接口的超时时间

int IOT_MQTT_Unsubscribe(void *handle, const char *topic_filter)			//向云端取消订阅指定的topic
	handle		MQTT句柄,可为NULL
	topic_filter	需要取消订阅的topic


int IOT_MQTT_Publish(void *handle, const char *topic_name, iotx_mqtt_topic_info_pt topic_msg)	//向指定topic推送消息
	handle			MQTT句柄,可为NULL
	topic_name		接收此推送消息的目标topic
	topic_msg		需要推送的消息

int IOT_MQTT_Publish_Simple(void *handle, const char *topic_name, int qos, void *data, int len)		//向指定topic推送消息
	handle		MQTT句柄,可为NULL
	topic_name	接收此推送消息的目标topic
	qos		采用的QoS策略
	data		需要发送的数据
	len		数据长度






















