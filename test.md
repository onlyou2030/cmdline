```c++
int main(int argc,char* argv[])
{
    cmdline::parser parser;
    parser.add<std::string>("addr", 'a', "sfu addr", true);
    parser.add("echo", 'e', "is echo");
    parser.add("directsfu", 'd', "is direct connect sfu");
    parser.add<uint32_t>("stime", 's', "single time", true);
    parser.add<uint32_t>("itime", 'i', "interval time", true);
    parser.add<int32_t>("number", 'n', "num of testing times", false, -1);
    parser.add<uint32_t>("subvideo", 'v', "num of subscribe video", false, 1);
    parser.add<std::string>("roomid", 'r', "room id", false, "");
    parser.parse_check(argc, argv);

    vcs::sdk::MeetingAgentManager fakeAgentManager(parser);
    return 0;
}
```



```c++
    , _addr(parser.get<std::string>("addr"))
    , _intervalTime(parser.exist("itime") ? parser.get<uint32_t>("itime") : -1)
    , _runTime(parser.exist("stime") ? parser.get<uint32_t>("stime") : -1)
    , _subscribeNum(parser.exist("subvideo")?parser.get<uint32_t>("subvideo"):1)
    , _runCount(parser.exist("number") ? parser.get<int32_t>("number") : 1)//if don't have "number". will run only once
    , _echo(parser.exist("echo") ? true : false)
    , _isSfu(parser.exist("directsfu") ? true : false)
    , _roomid(parser.exist("directsfu") ? parser.get<std::string>("roomid") : std::string())
    , _logger(Poco::Logger::get("MeetingAgentManager"))
```

