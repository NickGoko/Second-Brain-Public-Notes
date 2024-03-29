---
tags:
  - cloud/aws
---

![](https://i.imgur.com/n9myfpp.png)

Amazon Elastic Transcoder is <mark style="background: #ADCCFFA6;">a highly scalable, easy to use and cost-effective way for developers and businesses to convert (or “transcode”) video and audio files from their source format into versions that will playback on devices like smartphones, tablets and PCs</mark>.

Supports a wide range of input and output formats, resolutions, bitrates, and frame rates.

Also offers features for automatic video bit rate optimization, generation of thumbnails, overlay of visual watermarks, caption support, DRM packaging, progressive downloads, encryption and more.

Picks up files from an input S3 bucket and saves the output to an output S3 bucket.

Uses a JSON API, and SDKs are provided for Python, Node.js, Java, .NET, PHP, and Ruby.

Provides transcoding presets for popular formats.

You are charged based on the duration of the content and the resolution or format of the media.

# FAQ
## General

**Q: What is Amazon Elastic Transcoder?**

Amazon Elastic Transcoder is a highly scalable, easy to use and cost effective way for developers and businesses to convert (or “transcode”) video and audio files from their source format into versions that will playback on devices like smartphones, tablets and PCs.

**Q: What can I do with Amazon Elastic Transcoder?**

You can use Amazon Elastic Transcoder to convert video and audio files into supported output formats optimized for playback on desktops, mobile devices, tablets, and televisions. In addition to supporting a wide range of input and output formats, resolutions, bitrates, and frame rates, Amazon Elastic Transcoder also offers features for automatic video bit rate optimization, generation of thumbnails, overlay of visual watermarks, caption support, DRM packaging, progressive downloads, encryption and more. For more details, please visit the [Product Details](http://aws.amazon.com/elastictranscoder/details/) page.  

#### Get Started with AWS for Free

[Create a Free Account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html)  
[Or Sign In to the Console](https://console.aws.amazon.com/elasticache/home)

___

AWS Free Tier includes 750hrs of Micro Cache Node with Amazon ElastiCache.  

[View AWS Free Tier Details »](https://aws.amazon.com/free/)  

**Q: Why should I use Amazon Elastic Transcoder?**

Amazon Elastic Transcoder manages all the complexity of running media transcoding in the AWS cloud. Amazon Elastic Transcoder enables you to focus on your content, such as the devices you want to support and the quality levels you want to provide, rather than managing the infrastructure and software needed for conversion. Amazon Elastic Transcoder scales to handle the largest encoding jobs. As with all Amazon Web Services, there are no up-front investments required, and you pay only for the resources that you use. We offer a free tier that enables you to explore the service and transcode up to up to 20 minutes of SD video or 10 minutes of HD video a month free of charge. To see terms and additional information on the free tier program, please visit the [AWS Free Usage Tier page](https://aws.amazon.com/free/).

**Q: How do I get started with Amazon Elastic Transcoder?**

You can sign up for Amazon Elastic Transcoder through the [AWS Management Console](https://console.aws.amazon.com/elastictranscoder/). You can then use the console to create a pipeline, set up an IAM role, and create your first transcoding job. To help you test Amazon Elastic Transcoder, the first 20 minutes of SD content (or 10 minutes of HD content) transcoded each month is provided free of charge. Once you exceed the number of minutes in this free usage tier, you will be charged at the prevailing rates. We do not watermark the output content or otherwise limit the functionality of the service, so you can use it and truly get a feel for its capabilities. To see terms and additional information on the free tier program, please visit the [AWS Free Usage Tier page](https://aws.amazon.com/free/). If you do not have an AWS account, you can create one by clicking the Sign Up button at the top of this page.

**Q: How do I use Amazon Elastic Transcoder?**

To use Amazon Elastic Transcoder you need to have at least one media file in an Amazon S3 bucket. The easiest way to use Amazon Elastic Transcoder is to try it through the console. Create a transcoding pipeline that connects the input Amazon S3 bucket to the output Amazon S3 bucket. Create a transcoding job that will transcode your media file, choose a transcoding preset (a template), and submit the job. Your transcoded file will appear in your output bucket once it has been processed.

**Q: What tools and libraries work with Amazon Elastic Transcoder?**

Amazon Elastic Transcoder uses a JSON API, and we provide SDKs for Python, Node.js, Java, .NET, PHP, and Ruby. The new [AWS Command Line Interface](https://aws.amazon.com/cli/) also supports Amazon Elastic Transcoder. You can see a full list of our SDKs [here](https://aws.amazon.com/tools/).  

**Q: Can I use the AWS Management Console with Amazon Elastic Transcoder?**

Yes. Amazon Elastic Transcoder has a console that is accessed through the AWS Management Console. You can use our console to create pipelines, jobs, and presets as well as manage and view existing pipelines and jobs.

**Q: How do I get my media files into Amazon S3?**

There are many ways to get content into Amazon S3, from the simple web-based uploader in the [AWS Management Console](https://console.aws.amazon.com/elastictranscoder/) to programmatic approaches through APIs. For very large files, you may wish to use [AWS Import/Export](https://aws.amazon.com/snowball/), [AWS Direct Connect](https://aws.amazon.com/directconnect/), or file-acceleration solutions available in the [AWS Marketplace](https://aws.amazon.com/marketplace). For more information please refer to the [Amazon S3 documentation](https://aws.amazon.com/documentation/s3/) and the [AWS Digital Media](https://aws.amazon.com/digital-media/) website.  

**Q: How do I retrieve my media files from Amazon S3?**

You can retrieve files from Amazon S3 programmatically, using the AWS Management Console or a third party tool. You can also mark Amazon S3 objects as public and download them directly from Amazon S3.

**Q: Can I use a Content Distribution Network (CDN) to distribute my media files?**

Yes. You can easily use CDNs to distribute your content; for example, you can use Amazon CloudFront to distribute your content to end-users with low latency, high data transfer speeds, and no commitments. You can use an output bucket that contains your transcoded content in Amazon S3 as the origin server for Amazon CloudFront. For more information, please visit the detail page for [Amazon CloudFront](https://aws.amazon.com/cloudfront/).

**Q: How long does it take to transcode a job?**

Jobs start processing in the order in which they are received in a pipeline. Once a job is ready to be transcoded, many variables affect the speed of transcoding, for example, the input file size, resolution, and bitrate. For example, if you were to submit a 10 minute video using the iPhone 4 preset, it would take approximately 5 minutes. If a large number of jobs are received they are backlogged (queued). Please note that the transcoding speed may be different between regions.

**Q: When will my job be ready?**

You can use Amazon SNS notifications to be informed of job status changes. For example, you can be notified when your job starts to transcode and when it has finished transcoding. For more information on Amazon SNS notifications, please see the detail page on [Amazon SNS](https://aws.amazon.com/sns/).

**Q: How many jobs are processed at once?**

Pipelines operate independently from one another. Each pipeline processes jobs in parallel up to a default limit set for that pipeline. Within a job, each individual output also progresses in parallel. For more information on limits and capacity, visit the [limits section](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/limits.html) in the Elastic Transcoder Developer Guide. You can request higher limits by opening a [support case](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=service-limit-increase&limitType=service-code-elastic-transcoders).

**Q: How many jobs can I submit?**

Currently, we allow a maximum of 100,000 jobs per pipeline. Once you exceed this limit, you will receive a 429 Rate Limit Exception. If you require this limit to be raised, please contact us [here](http://aws.amazon.com/contact-us/elastictranscoder-request/).

**Q: Can I create multiple outputs per job?**

Each transcoding job relates to a single input file and can create one or more output files. For example, you may wish to create audio only, lowand high-resolution renditions of the same input file and could do so as part of a single transcoding job. The number of outputs per job is limited. For more information on Amazon Elastic Transcoder limits, please refer to the documentation.

Multiple outputs are charged individually: each output is charged as a separate transcode.

**Q: How do I generate clips?**

You can create a clip from your source media in your transcoding job. You specify a start time and a duration (both specified as HH:mm:ss.SSS or sssss.SSS.) To cut off the start of a file, you would just specify a start time. You can generate different length clips (or transcode the entire file) for each different output in your transcoding job. You will be charged based on the output duration of your transcode, so if you have a five-minute input file and you create a one-minute output from it, you will only be charged for one minute of transcoding. Please remember that fractional minutes are rounded up, so if you create a clip that is one minute and thirty seconds in duration, you will be charged for two minutes of transcoding.

**Q: How do I stitch clips?**

You can specify two or more input files that need to be stitched to create a single output file in your transcoding job. Input files are stitched in the order they are specified. So if you want to add a bumper to your video, specify the bumper file as the first input and your video file as the second input. For each input, you can specify a Start Time and a Duration, which allows you to stitch together only the parts of each input that you want included in the output. You will be charged for the output duration of your transcode, so if you are stitching two five-minute input files to create a ten-minute output, you will be charged for ten minutes of transcoding.

**Q: What is a transcoding pipeline, what can I use it for, and how many can I have?**

A pipeline is a queue-like structure that manages your transcoding jobs. A pipeline can process multiple jobs simultaneously, and generally starts to process jobs in the order in which you added them to the pipeline. Jobs often finish in a different order based on job specifications. It is up to you how you wish to use pipelines. Some examples include submitting jobs to different pipelines based on the priority or the duration of a transcode, or using different pipelines for your development, test and production environments. The number of pipelines per AWS account is limited. For more information on Amazon Elastic Transcoder limits, please refer to the [documentation](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/limits.html).  

**Q: What are transcoding presets?**

A preset is a template that contains the settings that you want Amazon Elastic Transcoder to apply during the transcoding process, for example, the codec and the resolution that you want in the transcoded file. When you create a job, you specify which preset you want to use. We provide presets that create media files that play on any device and presets that target specific devices. For maximum compatibility, choose a “breadth preset” that creates output that plays on a wide range of devices. For optimum quality and file size, choose an “optimized preset” that creates output for a specific device or class of devices.

**Q: What do I do if none of your transcoding presets work for me?**

You can create your own custom presets based on an existing preset. Once you create your own custom preset, it is available across your AWS account for the Amazon Elastic Transcoder service within a specific region. For more information on presets, please refer to the [Amazon Elastic Transcoder Developer Guide](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/working-with-presets.html). The number of pipelines per AWS account is limited. For more information on Amazon Elastic Transcoder limits, please refer to the [documentation](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/limits.html).  

**Q: Why do I need to assign a role to a transcoding pipeline?**

Amazon Elastic Transcoder uses AWS Identity and Access Management (IAM) roles to enable you to securely control access to your media assets. The IAM role sets a policy that defines what permissions you have for accessing Amazon S3 resources. You can assign different roles to different pipelines, and an IAM administrator can create specific roles for use with Amazon Elastic Transcoder. More information about IAM can be found [here](https://aws.amazon.com/iam/).

**Q: How can I configure roles to be more restrictive?**

You can use the AWS Management Console to edit and create new IAM roles. IAM roles that are created by Amazon Elastic Transcoder are visible in the AWS Management Console and can also be edited.

**Q: How do I use notifications?**

Amazon Elastic Transcoder uses Amazon SNS to notify you of specific events. You can choose to be notified about jobs that start to process, jobs that complete, warnings, and errors. Each event type is assigned to an SNS topic, and you can use the same topic or different topics for each event. The Amazon Elastic Transcoder console will create an SNS topic for you or you can specify an existing one.

**Q: Why should I use notifications?**

Notifications are a much more efficient way to check transcoding status than polling the API. Notifications provide a way to be notified on specific events that occur in the system. For example, you can be notified on a completed event. This is useful if you want to know when a job has finished transcoding and this is far more efficient than calling the 'List Jobs By Status' or 'Read Job' API at regular intervals.

**Q: Why does my job keep failing?**

The most common reason for jobs to fail is that the input file is corrupted in some way. If you receive an error about the format not being supported, we are unable to decode your source file and we’d love for you to tell us more about on our [Discussion Forum](https://forums.aws.amazon.com/forum.jspa?forumID=147). We need the following information to assist with diagnosis: AWS Account ID, Region and Job ID. For a list of error codes, please refer to the [documentation](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/error-handling.html).  

**Q: How can I generate more than one thumbnail per job?**

You can specify a thumbnail creation interval in seconds to create one thumbnail every n seconds. To create thumbnails in more than one size, you need to create different jobs.

**Q: Can I reserve a transcoder for my exclusive use?**

Amazon Elastic Transcoder provides a shared transcoding service and does not enable a transcoder to be reserved or allocated to an individual customer.

**Q: Do I need to pay license fees?**

We have licensed relevant intellectual property from the applicable patent pools for transcoding content. Like any other transcoder, customers are responsible for evaluating and, if necessary, securing licenses for distribution of content in various formats.

**Q: Do you support live encoding?**

Amazon Elastic Transcoder is a file-based transcoding service and does not support live transcoding.

**Q: Are there limits to the service?**

The number of transcoding pipelines, transcoding presets and outputs per job have limits. Most of these limits can be adjusted on a customer-by-customer basis. For the current limits, please refer to the [documentation](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/limits.html).  

**Q: How do I increase service limits?**

If you require an increase in the service limits, please contact us [here](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=service-limit-increase&limitType=service-code-elastic-transcoders) and provide all the information requested on the form. We will then contact you to discuss your requirements.  

**Q: Where is Amazon Elastic Transcoder available?**

Amazon Elastic Transcoder is available in the following AWS regions: US East (N Virginia), US West (Oregon), US West (N California), EU (Ireland), Asia Pacific (Tokyo), Asia Pacific (Singapore), Asia Pacific (Sydney), and Asia Pacific (Mumbai).

The service operates standalone in each region, so jobs created in one region may not be transferred to another region.

You can create a transcoding pipeline in one region that would specify Amazon S3 buckets in another region. However, if you choose to do this, you should be aware that you will incur Amazon S3 transfer costs when content is read from or written out to an Amazon S3 bucket in a region other than the one where the transcoding work is taking place.  

**Q: Can I pass metadata when creating a job?**

You have the option to attach up to 10 custom metadata key-value pairs to your Elastic Transcoder jobs. This metadata will be included in the job notifications and when reading the job via the API or console. You provide this information in the “UserMetadata” field on the Job object.

___

## Format Support

**Q: What input formats do you support?**

We support popular web, consumer and professional media formats. Examples include 3GP, AAC, AVI, FLV, MP4 and MPEG-2. If there is a format that you’ve found does not work, please let us know through our forum.

**Q: Where can I find a comprehensive list of support formats?**

We add new input formats on an ongoing basis, so such a list would age quickly. Please take advantage of our free tier and console to try a format not mentioned above and if you run into problems, please let us know!

**Q: When creating MP4 files, do you support "fast start"?**

We locate the MOOV atom for an MP4 at the start of the file so that your player can start playback immediately without waiting for the entire file to finish downloading.

**Q: Do you support Apple ProRes or digital cinematography formats?**

We do not support reading Apple ProRes files or raw camera formats like ARRI and RED at this time.

**Q: What video formats can I transcode into?**

We support the following video codecs: H.264, VP9, VP8, MPEG-2, and animated GIF. File formats supported include MPEG-2 TS container (for HLS), fmp4 (for Smooth Streaming and MPEG-DASH), MP4, WebM, FLV, MPG, and MXF (XDCAM-compatible). For information on file formats that are supported by specific codecs, please visit the [Product Details](http://aws.amazon.com/elastictranscoder/details/) page.  

**Q: What audio formats can I transcode into?**

We support the following audio codecs: AAC, MP3, MP2, PCM, FLAC, and Vorbis. Audio-only file formats supported include MP3, MP4, FLAC, OGA, OGG, and WAV. For information on file formats that are supported by specific codecs, please visit the [Product Details](http://aws.amazon.com/elastictranscoder/details/) page.  

**Q: How is album art supported for audio files?**

Album art is supported in MP4 files containing AAC audio, in MP3 files, and in FLAC files. Album art is not supported for OGA, OGG, WAV, WebM or MPEG-2 TS outputs. You can specify whether album art from the source file is passed through to the output, removed, or whether new album art should replace it or be appended to it.

**Q: How do I create an audio file from a video file?**

To strip out video and create an output that only contains the audio track, run a transcoding job with your input file and use one of the system transcoding presets that contains Audio in its name. Alternatively, you can create your own audio only custom transcoding preset. The output file will only contain the audio portion of the input file.

**Q: Do you support surround sound formats?**

The audio portion of the transcoded output from Amazon Elastic Transcoder is two-channel AAC, MP3 or Vorbis.

**Q: Do you support audio channel remapping?**

If the source file contains multi-channel audio, the output will contain the first two channels, which are frequently left and right audio tracks. For the MXF container, we support multiple modes of packaging the audio into the file, including optional insertion of motor only shots (MOS).

**Q: Can I generate XDCAM-compatible video?**

Yes, the easiest way to generate XDCAM-compatible outputs is to specify one of the XDCAM system presets when creating a transcoding job. You can also create a custom preset by choosing the MXF container with MPEG-2 video and PCM audio.

**Q: Do you support closed captions?**

Yes, you can add, remove, or preserve captions as you transcode your video from one format to another.

Supported input formats:  
Embedded: CEA-608, CEA-708 (MPEG-2 only) and mov-text  
Sidecar captions: DFXP, EBU-TT, SCC, SMPT, SRT, TTML, WebVTT

Supported output formats:  
Embedded captions: mov-text (MP4), and CEA-708 (MP4 and MPEG-TS)  
Sidecar captions: DFXP, EBU-TT, SCC, SMPT, SRT, TTML, and WebVTT

CEA-708 captions are embedded in the H.264 SEI user data of the stream.  

**Q: Can you support multiple caption tracks?**

Yes, you can add one track per language.  

**Q: How do I create content for HLS output?**

There are two steps:

1. Create a transcoding job containing outputs for each variation using one of our supplied system presets or your own, based on the MPEG-2 TS container and H.264 and AAC codecs. The lowest rate stream should be an audio only stream.
2. Specify that the transcoding job create a playlist that references the outputs. You should order your bit rates from lowest to highest, with the audio only stream last, since this order will be maintained in the generated playlist file. Once your transcoding job has completed, the output bucket will contain a proper arrangement of your master and individual M3U8 playlists, and MPEG-2 TS media stream fragments.

Note: When selecting the HLSv4 option, your outputs should be matched to audio-only and video-only presets. For system presets, these can be identified by words "Audio" or "Video" as part of their name. For example, “System preset: HLS Video – 600k,” would match with the HLSv4 option whereas "System preset: HLS – 600k,” would be used with the HLSv3 option.

**Q: How do I create content for Smooth Streaming?**

There are two steps:

1. Create a transcoding job containing outputs for each variation using one of our supplied system presets or your own, based on the fragmented MP4 container and H.264 and AAC codecs.
2. Specify that the transcoding job create a playlist that references the outputs. Once your transcoding job has completed, the output bucket specified by the transcoding pipeline will contain your manifest ISM file, client ISMC file, and fragmented MP4 media files.

**Q: How do I create content for MPEG-DASH streaming?**

There are two steps:

1. Create a transcoding job containing the video-only outputs (with the desired resolutions and bitrates) and the audio-only output using either the system presets or your own customized presets, based on the fragmented MP4 container with H.264 video and AAC audio.  
    
2. Create an MPEG-DASH playlist for the transcoding job by selecting MPEG-DASH as the Playlist Format. Specify the outputs that this playlist will reference. Once your transcoding job has completed, the output bucket specified by the transcoding pipeline will contain your manifest MPD file, and the fragmented MP4 media files.

**Q: Should I use the HLSv3 or the HLSv4 option?**

HLS version 3 has been supported natively on iOS 2+ devices since July 2008 and on Android 4.0+ since Oct. 2011. HLS version 4 has been supported natively on iOS 5+ devices since Oct. 2011 and on Android 4.4+ since Sept. 2013.

If you able to reach your target devices with HLS version 4, you will be able to generate playlists that use byte range requests, late-binding audio, and I-frame only playback. Playlists with byte range requests are able to use just one file per bit rate, eliminating the need to manage thousands of small segment files. Late-binding audio allows the audio to be streamed separately from the video, eliminating redundant audio storage. I-frame only playback enables trick-play modes used to enhance fast-forward, rewind, and seeking through the video.

**Q: Can I stream HLS directly from S3?**

Yes, you can play your HLS renditions directly from S3 by pointing the player to the M3U8 playlist. We recommend you use a CDN such as Amazon CloudFront, which provides a better end user experience with improved scalability and performance. See [Configuring On-Demand Apple HTTP Live Streaming (HLS)](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/on-demand-streaming-hls.html).

**Q: Do I need a streaming server to deliver my Smooth Streaming content?**

Usually playing back Smooth Streaming requires an IIS origin server, and you cannot stream directly from S3. However, if you distribute your content with CloudFront you can simply configure a CloudFront Smooth Streaming distribution, eliminating the need for a streaming server. See [Configuring On-Demand Smooth Streaming](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/on-demand-streaming-smooth.html).

**Q: Why is the codec parameter that I want to change not exposed by the API?**

In designing Amazon Elastic Transcoder, we wanted to create a service that was simple to use. Therefore, we expose the most frequently used codec parameters. If there is a parameter that you require, please let us know by letting us know through our forum.

**Q: What settings do I use to preserve the dimensions of my video?**

Use the following settings in your custom preset:  
MaxWidth: auto; MaxHeight: auto; SizingPolicy: ShrinkToFit; PaddingPolicy: NoPad; DisplayAspectRatio: auto

**Q: How do I scale my output to a specified width and set the height to preserve the aspect ratio of the source content?**

Use the following settings in your custom preset:  
MaxWidth: \[Desired Width\]; MaxHeight: auto; SizingPolicy: Fit; PaddingPolicy: NoPad; DisplayAspectRatio: auto

**Q: How do I limit the height or width of a video without stretching the output to fit my set limit while preserving the input aspect ratio?**

Use the following settings in your custom preset:  
MaxWidth: \[Desired Width Limit\]; MaxHeight: \[Desired Height Limit\]; SizingPolicy: ShrinkToFit; PaddingPolicy: NoPad; DisplayAspectRatio: auto

**Q: What settings should I use to create a preset that causes the output video to fill the screen without distortion, if necessary cropping some of the edges ("center cut")?**

Use the following settings in your custom preset:  
MaxWidth: \[Desired Width\]; MaxHeight: \[Desired Height\]; SizingPolicy: Fill; PaddingPolicy: NoPad; DisplayAspectRatio: auto

**Q: What settings should I use to create a preset that causes the output video to fill the screen without cropping any image area, if necessary distorting the image ("squeeze" or "stretch")?**

Use the following settings in your custom preset:  
MaxWidth: \[Desired Width\]; MaxHeight: \[Desired Height\]; SizingPolicy: Stretch; PaddingPolicy: NoPad; DisplayAspectRatio: auto

**Q: How do I make my watermark scale with my video?**

In the watermark settings of your transcoding preset, set the HorizontalAlign, VerticalAlign, and Target parameters as desired. Then set the HorizontalOffset and VerticalOffset with relative parameters. For example, to place the watermark 10% away from the edges, set both values to 10%.

**Q: How do I avoid distorting my watermark?**

If you do not want your watermark to be distorted when the video output is resized, set the SizingPolicy to ShrinkToFit while setting MaxWidth and MaxHeight to 100%. With these settings, Elastic Transcoder will never up-sample, expand, or distort your watermark.

**Q: What are the settings for placing my watermark over the active video region rather than over the matte?**

To place your watermark so that it is always over the active video content, use relative size for the MaxWidth and MaxHeight settings, and set the Target to be Content. For example, to fix the watermark size to 10% of the active output video size, set both MaxWidth and MaxHeight to 10%.

**Q: How do I use multiple watermarks?**

Presets specify placement settings for up to four watermarks. Each setting has an associated watermark ID. You can create a job with up to four watermarks by specifying an array of watermarks in the job creation call. Each element of the array specifies the Id of the watermark setting to use, and the watermark image file.  

**Q: Can I generate NTSC or PAL outputs?**

Yes, you can generate both NTSC and PAL compliant outputs. The easiest way to generate NTSC and PAL compliant outputs is to specify the NTSC or PAL system preset when creating a transcoding job. Via the console, this is done by the preset drop down for each output of your transcoding job.  

## Pricing

**Q: How much does Amazon Elastic Transcoder cost to use?**

Pricing for Amazon Elastic Transcoder is described here. Our pricing does not require any commitment or minimum volume of jobs. We also offer a free tier that enables you to explore the service and transcode up to up to 20 minutes of audio-only output, 20 minutes of SD video output and 10 minutes of HD video output a month free of charge. To see terms and additional information on the free tier program, please visit the AWS Free Usage Tier page.

**Q: How are jobs charged?**

Transcoding jobs are charged according to the duration of the content. For example, media that lasts 60 minutes costs twice as much as media that lasts 30 minutes. High definition (HD) content costs twice as much as standard definition (SD). Audio-only output is priced lower than standard definition (SD) output. The minimum charge for a job is one minute. We do not charge for thumbnail generation, for API calls, or for Amazon S3 transfer within the same region. For more information, please refer to the Amazon Elastic Transcoder [pricing page](https://aws.amazon.com/elastictranscoder/pricing/).

**Q: How are fractional minutes charged?**

Fractional minutes are rounded up. For example, if your output duration is less than a minute, you are charged for one minute. If your output duration is 1 minutes and 10 seconds, you are charged for 2 minutes.

**Q: Do you charge for failed jobs?**

Our policy is to forgive customers for failed jobs unless the number of failed jobs becomes excessive.

**Q: Is it cheaper to use multiple outputs per job than to use separate jobs?**

When you use multiple outputs per job, transcoding costs remain the same as if you had submitted multiple jobs for each output. However, the processing time will be quicker for larger jobs since the source file is only being transferred from your S3 bucket to Amazon Elastic Transcoder once.  

**Q: Do your prices include taxes?**

Except as otherwise noted, our prices are exclusive of applicable taxes and duties, including VAT and applicable sales tax. For customers with a Japanese billing address, use of AWS services is subject to Japanese Consumption Tax. [Learn more](https://aws.amazon.com/c-tax-faqs/).

## Security

**Q: Are my media assets secure?**

You are in complete control of your media assets because they are stored in your own Amazon S3 buckets. You use IAM roles to grant us access to your specific Amazon S3 bucket.

**Q: Can I set S3 permissions and storage options?**

Amazon Elastic Transcoder enables you to specify which users, groups, and canonical IDs you want to grant access to your transcoded files, thumbnails and playlists, as well as the type of access that you want them to have. You can also specify whether to store transcoded content using Standard or Reduced Redundancy Storage. Please refer to [Amazon Elastic Transcoder documentation](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/api-reference.html) for further information.

**Q: Can I use encrypted input media files or encrypt my output files?**

Yes. You can use encrypted mezzanine files as input to Amazon Elastic Transcoder, or protect your transcoded files by letting the service encrypt the output. Supported options range from fully managed integration with [Amazon S3's Server-Side Encryption](http://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html), to keys that you manage on your own and protect using [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/). Furthermore, encryption support is not limited to your video files. You can protect thumbnails, captions, and even watermarks.

**Q: Do you support DRM?**

Yes, we support packaging for Microsoft PlayReady DRM. Our Smooth Streaming packaging is compatible with the Microsoft PIFF 1.1, and our HLSv3 packaging is compatible with the Discretix 3.0.1 specification for Microsoft PlayReady.

**Q: Can I get a history of all Amazon Elastic Transcoder API calls made on my account for security, operational or compliance auditing?**

Yes. To start receiving a history of all Elastic Transcoder API calls made on your account, you simply turn on AWS CloudTrail in [CloudTrail's AWS Management Console](https://console.aws.amazon.com/cloudtrail). For more information, visit the [AWS CloudTrail home page](http://aws.amazon.com/cloudtrail/).

**Q: Do I need to setup AWS KMS before using the Elastic Transcoder encryption and DRM packaging features?**

Yes. You must first create a master AWS KMS key and add the role used by Elastic Transcoder as an authorized user of that key. Elastic Transcoder uses your KMS master key to protect the data encryption keys that it exchanges with you.

**Q: Can I save the keys used to encrypt my HLS streams to S3?**

Yes. If you elect to store your keys in S3, Elastic Transcoder will write your keys to the same folders as your playlist files, and your keys will be protected using Server-Side Encryption with Amazon S3-Managed Encryption Keys ([SSE-S3](http://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html)).

**Q: Can I rotate the keys used for HLS with AES-128 encryption?**

Key rotation is not supported. All renditions and file segments share the same key.