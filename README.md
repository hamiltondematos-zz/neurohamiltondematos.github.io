# hamiltondematos.github.io


Para problemas do tipo 
mean shape incompatible with input shape

Let go to line 253-254 in caffe/python/caffe/io.py Replace

if ms != self.inputs[in_][1:]:
    raise ValueError('Mean shape incompatible with input shape.')
By

if ms != self.inputs[in_][1:]:
    print(self.inputs[in_])
    in_shape = self.inputs[in_][1:]
    m_min, m_max = mean.min(), mean.max()
    normal_mean = (mean - m_min) / (m_max - m_min)
    mean = resize_image(normal_mean.transpose((1,2,0)),in_shape[1:]).transpose((2,0,1)) * (m_max - m_min) + m_min
    #raise ValueError('Mean shape incompatible with input shape.')
