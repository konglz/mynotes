
# Java项目规范化

## 日志

* 业务日志放在独立的logger下
把日级级别降到debug，追查业务流程问题，发现框架的debug日志暴涨，一下子把业务debug日志淹没了……
因此，想给业务日志单独设置logger。
