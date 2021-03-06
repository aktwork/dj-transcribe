# SaaS frontend built with Django

It is django-based frontend for Natural Language Processing service dealing with Pytube API and Stripe.
Customers check youtube video link from the home page and transcribe it with an easy to use UI. The payments for the transcription service is implemented by Stripe API. So you need to put Stripe keys which are publish key and secret key in the Django settings.py or load those at runtime.
This app is ready to deploy to heroku which is free and easy hosting and deployment service.
For deployment, you may need to intall [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli).
Once you installed heroku cli in your machine, please follow steps below.

test credit card: 4242 4242 4242 4242

## Deployment

First, you need to clone repository.
```
git clone https://github.com/wiseinvoker/django-saas-api.git
cd django-saas-api
```
Then, create your heroku app.
```
heroku create
```
If you created your heroku app, you can check it using `git remote -v`
```
git remote -v
```
And then push to the heroku.
```
git push heroku master
```
Now the app is deployed to heroku.

For more information, visit [Deploying with Git](https://devcenter.heroku.com/articles/git) and [Working with Django](https://devcenter.heroku.com/categories/working-with-django).


## S3 Bucket

* Create S3 bucket with public permissions
* Create IAM user (programmatic user)
* Create a custom IAM policy

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:GetObjectAcl",
                "s3:GetObject",
                "s3:ListBucket",
                "s3:DeleteObject",
                "s3:PutObjectAcl"
            ],
            "Resource": [
                "arn:aws:s3:::transcribe-now/*",
                "arn:aws:s3:::transcribe-now"
            ]
        }
    ]
}
```

* Test config (eu-west-3, json)

```
aws config
aws s3 ls s3://transcribe-now
aws s3 cp data.pdf s3://transcribe-now
```


# Crontab

Reoccuring jobs are schedule via the `django-crontab` module (https://pypi.org/project/django-crontab/).

The following commands to move defined `CRONJOBS` in `settings.py` to crontab.

```
python manage.py crontab add
python manage.py crontab show
python manage.py crontab remove
```

To run the respective commands on heroku.

```
heroku run python manage.py crontab add
heroku run bash
```