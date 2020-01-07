FROM ubuntu
COPY script1.7.sh .
RUN chmod +x script1.7.sh
RUN apt-get update && apt-get install -y curl
CMD ["./script1.7.sh"]