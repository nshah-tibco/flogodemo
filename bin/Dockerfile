# You can replace or modify this Dockerfile as per your requirements
# DO NOT CHANGE or REMOVE 'COPY ./flogoapp /app/flogoapp'
FROM amazonlinux:2
WORKDIR /app
COPY ./flogoapp /app/flogoapp
RUN chmod +x flogoapp
ENTRYPOINT ["/app/flogoapp"]
