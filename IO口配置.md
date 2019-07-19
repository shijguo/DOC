                                IO口配置

    #define GPIO_OUTPUT_IO_0    15
    #define GPIO_OUTPUT_IO_1    16
    #define GPIO_OUTPUT_PIN_SEL  ((1ULL<<GPIO_OUTPUT_IO_0) | (1ULL<<GPIO_OUTPUT_IO_1))

    gpio_config_t io_conf;                          //创建句柄
    io_conf.intr_type = GPIO_INTR_DISABLE;          //失能IO中断
    io_conf.mode = GPIO_MODE_OUTPUT;                //输出模式
    io_conf.pin_bit_mask = GPIO_OUTPUT_PIN_SEL;     //映射
    io_conf.pull_down_en = 0;                       //下拉模式失能
    io_conf.pull_up_en = 0;                         //上拉模式失能
    gpio_config(&io_conf);                          //IO口初始化


还有一些IO中断API

    /* 设置中断类型  */
    gpio_set_intr_type(GPIO_INPUT_IO_0, GPIO_INTR_ANYEDGE);
    /* 删除相应IO口的中断处理 */
    gpio_isr_handler_remove(GPIO_INPUT_IO_0);
    /* 为相应的IO口增加中断处理  */
    gpio_isr_handler_add(GPIO_INPUT_IO_0, gpio_isr_handler, (void *) GPIO_INPUT_IO_0)

