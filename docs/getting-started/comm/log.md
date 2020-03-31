# nim_log

Ϊ��������־д��Ч�ʼ������ԣ���־ģ������ڴ�ӳ���ļ��ķ�ʽ�����ڴ��ļ���С�ﵽָ����Сʱ��һ����ˢ��ָ������־�ļ��������ٴ�����ʱ�����ȶ�ȡӳ���ļ������ӳ���ļ������ݣ���ˢ�뵽��־�ļ�
## ��־ģ���ʹ��

+ ������־����   
���� nim_log::NIMLog::CreateLogger() ��ȡһ����־����
+ ��Ҫ�ӿ�   


        class ILogger
        {
        public:
            virtual void SetLogFile(const std::string &file_path);//������־�ļ�·�� UTF8��ʽ�ַ���
            virtual std::string GetLogFile();//��ȡ��־�ļ�·��
            virtual void SetLogLevel(LOG_LEVEL lv);//������־���𣬵������ü������־�������
            virtual LOG_LEVEL GetLogLevel();//��ȡ��ǰ��־����
            virtual bool Flush();//�ڴ�ӳ���ļ�ˢ�뵽��־�ļ�
            virtual void Release();//�ͷ���ӳ����ڴ��ļ�
        };
+ д��־    
Ϊ���ڴ����з���д����־����־����ģ�鶨���˺�`__NIM_LOG_PRO`    
    - __NIM_LOG_PRO:

        __NIM_LOG_PRO(fmt,Logger)
        fmt: ��ӡ��־�ĸ�ʽ
        Logger:��־����
    - ��־��ʽ    
    ��־�еĲ�������ռλ������ʽ����������"`{`i`}`"�ĸ�ʽ,����������ķ�ʽ���ݸ���־����������ʾ    

            __NIM_LOG_PRO("kye/value {0}:{1}",logger) << key << value;
    - ʹ��ʾ��    
Ϊ���ڴ����и������ʹ����־���ܣ������Զ�`__NIM_LOG_PRO`�����ٴη�װ����    

            USING_NS_NIMLOG
            class TestLogger : public NS_EXTENSION::Singleton<TestLogger,false>
            {
                SingletonHideConstructor(TestLogger);
            private:
                TestLogger() :logger_(NIMLog::CreateLogger()) {}
                ~TestLogger() = default;
            public:
                inline const Logger& GetLogger() const {
                    return logger_;
                }
            private:
                Logger logger_;
            };
            #define TEST_LOG_PRO(fmt) __NIM_LOG_PRO(fmt,TestLogger::GetInstance()->GetLogger())
            #define TEST_LOG_APP(fmt) __NIM_LOG_APP(fmt,TestLogger::GetInstance()->GetLogger())
            #define TEST_LOG_WAR(fmt) __NIM_LOG_WAR(fmt,TestLogger::GetInstance()->GetLogger())
            #define TEST_LOG_ERR(fmt) __NIM_LOG_ERR(fmt,TestLogger::GetInstance()->GetLogger())
            #define TEST_LOG_KER(fmt) __NIM_LOG_KER(fmt,TestLogger::GetInstance()->GetLogger())
            #define TEST_LOG_ASS(fmt) __NIM_LOG_ASS(fmt,TestLogger::GetInstance()->GetLogger())
            #define TEST_LOG_INT(fmt) __NIM_LOG_INT(fmt,TestLogger::GetInstance()->GetLogger())



            .......


            TEST_LOG_PRO("kye/value {0}:{1}") << key << value;
