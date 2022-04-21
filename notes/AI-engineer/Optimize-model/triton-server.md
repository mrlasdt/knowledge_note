
# Triton

+ Features of triton server: 
  1. Concurrent model execution support: Multiple models (or multiple instances of the same model) can run simultaneously on the same GPU.
  2. Batching Support: Triton can deal with a batch of input request and its corresponding batch of predictions.
  3. Ensemble support
  4. Multi-GPU support. Triton can distribute inferencing across all system GPUs.
  5. Model repositories may reside on a locally accessible file system (e.g. NFS), in Google Cloud Storage, or in Amazon S3. (This feature plays a very important role if we want to deploy triton server on the cloud and make inference requests via the most popular Lambda Functions in case of AWS)
  6. Metrics indicating GPU utilization, server throughput, and server latency. The metrics are provided in the Prometheus data format.
  7. Model version support




# Reference
+ https://medium.com/nvidia-ai/how-to-deploy-almost-any-hugging-face-model-on-nvidia-triton-inference-server-with-an-8ee7ec0e6fc4