Neural networks are becoming increasingly popular in several domains, from image
recognition to natural language processing. In addition, neural networks are entering
safety-critical fields, such as autonomous driving. In these cases, it is crucial to
have a fast and reliable inference. It is then necessary to deeply understand a
specific model’s robustness and resilience. These days, neural network models are
also becoming bigger and more complex due to the higher number of parameters
and layers. Therefore, many techniques have been developed to reduce the model’s
size, such as pruning and quantization. These techniques allow the execution of the
model on edge devices, such as FPGA (Field Programmable Gate Arrays). In this
thesis, the focus is on quantized neural network models. Another core aspect when
dealing with edge device deployment is the design of the accelerator. Currently,
there are two main architectures: systolic arrays and dataflow. In general, the
characteristics of both accelerators are to parallelize computational tasks, such as
convolution, and speed up the inference of the model. This allows for obtaining very
high throughput on edge devices. The most significant advantage of the dataflow
architecture is that each network layer has a custom architecture with a custom
number of Processing Elements, contrary to the systolic array where all the layers
share the same computation units. Additionally, on dataflow architecture, the
access to the off-chip memory is minimized, significantly reducing latency with
respect to systolic arrays . On the contrary, systolic arrays allow for more flexibility
and do not require a different binary file to reconfigure the logic when the network
topology changes. This thesis focuses on Dataflow-style architectures. The most
significant contribution of this thesis is the development of a Fault Injector. This
module allows the injection of errors (soft errors, such as bit-flips) inside a specific
network layer to test how resilient networks, or parts of them, are. The critical
aspects considered when developing the Fault Injector are the smallest possible
footprint, low latency overhead, usability, and flexibility. All the modifications
were done directly on the FINN compiler (the chosen framework for generating
dataflow-style accelerators) to obtain higher usability and flexibility. . This ensured
tight integration with the framework and guaranteed the compatibility of the Fault
Injector with almost all already existing neural network models supported by FINN.
Another feature implemented to achieve maximum flexibility is the addition of
configurable parameters for the custom layer. The Fault Injector has some variables
that enable deep customizability. The end user can specify if the inputs of the layer
should be flipped; if the weights of the layer should be flipped; which bit should be
flipped; which operation is faulty and which is not; the frequency of the occurrence
of a fault . Moreover, these parameters are configurable at runtime thanks to a
simple JSON file, removing the need to re-synthesising the model. Small footprints
and low latency were achieved thanks to an optimized fault injection algorithm
and HLS tools, such as pragmas , which are special directives that can be used to
optimize the design, reduce latency, improve throughput performance, and reduce
area and device resource usage. All these optimizations allowed the building of
a faulty model of Mobilenet while still having some free LUTs and FFs. The
experiments shows how a faulty version of Mobilenet-v1 was build with a 24.1%
LUT and 18.8% FF overhead with respect to the original model. The observed
results show that the higher the flipped bit importance (MSB instead LSB) the
lower the final accuracy. Same behaviour is noticed when increasing the percentage
of faulty operations as well as their frequency. Another interesting result is the
comparison between flipping inputs or weights. In general, the experiments show
that the weights are more sensitive compared to the inputs.