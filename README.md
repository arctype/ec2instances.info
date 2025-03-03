# EC2Instances.info

![Vantage Picture](https://uploads-ssl.webflow.com/5f9ba05ba40d6414f341df34/5f9bb1764b6670c6f7739564_moutain-scene.svg)

> I was sick of comparing EC2 instance metrics and pricing on Amazon's site so I
> made [EC2Instances.info](https://ec2instances.info).

EC2Instances.info was originally created by [Garret
Heaton](https://github.com/powdahound), is now hosted by
[Vantage](https://vantage.sh/) and developed by the community of contributors.

## Project status

Vantage employees are actively maintaining and hosting the site with the help of
contributors here. Improvements in the form of pull requests or ideas via issues
are welcome!

People have suggested many neat ideas and feature requests by opening issues on
this repository. We also have a [Slack
Community](https://join.slack.com/t/vantagecommunity/shared_invite/zt-oey52myv-gq4AWRKkX25kjp1UGziPTw)
for anyone to join with a devoted channel named #instances-vantage.sh.

## Running locally

First, you'll need to provide credentials so that boto can access the AWS API.
Options for setting this up are described in the [boto
docs](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/configuration.html).
Ensure that your IAM user has at least the following permissions:

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "ec2:DescribeInstanceTypes",
                "Resource": "*"
            },
            {
                "Effect": "Allow",
                "Action": "pricing:*",
                "Resource": "*"
            }
        ]
    }

Specifically on boto you can run `aws configure` and input your AWS_ACCESS_KEY_ID
and your AWS_SECRET_ACCESS_KEY into the prompts. You will need these below.

## Running in Docker (recommended)

1. Clone the repository, if not already done:

        git clone https://github.com/vantage-sh/ec2instances.info
        cd ec2instances.info

1. Build a docker image:

        docker build --build-arg AWS_ACCESS_KEY_ID=<HI MOM> --build-arg AWS_SECRET_ACCESS_KEY=<HI DAD> -t ec2instances.info .

1. Run a container from the built docker image:

        docker run -d --name some-container -p 8080:8080 ec2instances.info

1. Open [localhost:8080](http://localhost:8080) in your browser to see it in action.

## Detailed local build instructions

Note: These instructions are only kept here for reference, the Docker
instructions mentioned above hide all these details and are recommended for
local execution.

Make sure you have LibXML and Python development files.  On Ubuntu, run `sudo
apt-get install python-dev libxml2-dev libxslt1-dev libssl-dev`.

Then:

    git clone https://github.com/vantage-sh/ec2instances.info
    cd ec2instances.info/
    python3 -m venv env
    source env/bin/activate
    pip install -r requirements.txt
    invoke build
    invoke serve
    open http://localhost:8080
    deactivate # to exit virtualenv

## Requirements

- Python with virtualenv
- [Invoke](http://www.pyinvoke.org/)
- [Boto](http://boto.readthedocs.org/en/latest/)
- [Mako](http://www.makotemplates.org/)
- [lxml](http://lxml.de/)

## API Access

The data backing EC2Instances.info has recently been made available via a free
API. All you need to get started is a free API key. To get started with API
access, check out the devoted [API
documentation](https://vantage.readme.io/reference/general).

## Keep up-to-date

Feel free to watch/star this repo as we're looking to update the site regularly.
Vantage also works on the following relevant projects:

- [The Cloud Cost Handbook](https://github.com/vantage-sh/handbook) - An
  open-source set of guides for best practices of managing cloud costs.
- [The AWS Cost Leaderboard](https://leaderboard.vantage.sh/) - A hosted site of
  the top AWS cost centers.
- [Vantage](https://vantage.sh/) - A cloud cost transparency platform.
