# Architecture of the system
![diagram-export-2-17-2024-2_46_36-PM](https://github.com/SufiyanGolandaz/notification-service/assets/42806710/8dcad0b6-9eb1-4e39-9bd3-7dc8c2478229)

## Explanation of Components

### Client
```bash
    -Notification service is called due to result of an event on client side.
    -For e.g user has updates something or user has made a transaction.
```

### Notification Service
```bash
    -This service is responsible for putting the notifications in the message queue.
    -It must implement the logic of filtering out targeted user based on some criteria (like if the user has opted to subscribe to the notif)
    -Has access to Notification Info table which helps in implementing the filter logic.
```
### Notification Info Database
```bash
    -SQL database:- reason we will be reading from it multiple times.
    -can have columns like user, targeted_user.
```
### Messaging Queue
```bash
    -To handle large number of requests, since there are multiple users and each users might have multiple subscribers.
    -We can implement multiple messaging queue based on priority of the message.
    -For e.g we can assign 1st priority to OTP verification messages, followed by transactional messages, followed by promotional messages.
    -We can use Kafka or SNS
```

### Email Service
```bash
    -It is responsible for sending emails to user.
    -It requires email id of the recipient, subject, email body to send, optional attachment.
    -We can use nodemailer, sendgrid.
```
### SMS Service
```bash
    -It is responsible for sending SMS to user.
    -It requires phone number of recipient and text body to send.
```
### Push Notification Service
```bash
    -It is responsible for sending push notification to user.
```

