FROM nvcr.io/nvidia/l4t-tensorrt:r8.4.1.5-devel

RUN apt update
RUN apt install -y python3-opencv \ 
        libopencv-dev \
        wget \
        git \
        build-essential

RUN git clone https://github.com/AlexeyAB/darknet

WORKDIR darknet

RUN mkdir /opt/videos

COPY test1.mp4 /opt/videos/test1.mp4
COPY obj.names ./data/obj.names
COPY obj.data ./data/obj.data
COPY train.txt ./data/train.txt
COPY test.txt ./data/test.txt
COPY yolov4-tiny-custom.cfg ./yolov4-tiny-custom.cfg
COPY yolov4-tiny-custom_best.weights ./yolov4-tiny-custom_best.weights

EXPOSE 8070
EXPOSE 8090

RUN make -j6 GPU=1 CUDNN=1 CUDNN_HALF=1 OPENCV=1

CMD ./darknet detector demo ./data/obj.data ./yolov4-tiny-custom.cfg ./yolov4-tiny-custom_best.weights /opt/videos/test1.mp4 -json_port 8070 -mjpeg_port 8090 -ext_output -dont_show

#EOF 

