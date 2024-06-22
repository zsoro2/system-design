# Chat app

- Daily active user: 50M
- Messages every day: 10 msg to 4 people

Totals:
Total messages a day: 50M x 40 = 2B / day
Total message storage a day: 2B x 100 bytes = 200GB/day 
Total files sent: 5 precent * 2B = 100M / day




## Database design


While you can mimic group functionality within a single chats table by using flags and additional logic, this approach can complicate your queries and may lead to scalability and maintainability issues as your application grows. Using separate groups and users_groups tables provides clearer separation of concerns, simplifies query logic, and offers greater flexibility for future enhancements. (e.g., roles within groups, group settings)

**users**

This table will contain a user's information such as name, phoneNumber, and other details.

**messages**

As the name suggests, this table will store messages with properties such as type (text, image, video, etc.), content, and timestamps for message delivery. The message will also have a corresponding chatID or groupID.

**chats**

This table basically represents a private chat between two users and can contain multiple messages.

**users_chats**

This table maps users and chats as multiple users can have multiple chats (N:M relationship) and vice versa.

**groups**

This table represents a group made up of multiple users.

**users_groups**

This table maps users and groups as multiple users can be a part of multiple groups (N:M relationship) and vice versa.


## Messaging

The pull model approach is not scalable as it will create unnecessary request overhead on our servers and most of the time the response will be empty, thus wasting our resources. To minimize latency, using the push model with WebSockets is a better choice because then we can push data to the client once it's available without any delay, given that the connection is open with the client.




[!ref target="blank" text="Whatsapp"](https://github.com/karanpratapsingh/system-design?tab=readme-ov-file#whatsapp)
[!ref target="blank" text="Long polling, Websockets"](https://www.karanpratapsingh.com/courses/system-design/long-polling-websockets-server-sent-events#long-polling)
