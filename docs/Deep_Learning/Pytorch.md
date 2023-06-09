# Pytorch基础

# 批量替换张量中的值

```python
import torch
a = torch.tensor((1, 2, 1, 4, 5))  # 1 2 1 4 5
print(a)
# 将a中等于1的地方替换为10
b = torch.where(a == 1, 10, a)  # 10 2 10 4 5
print(b)
```
# 点云归一化&反归一化
输入是一个(n, 3)的数据
```python
def pc_normalize(pc):
    """
    对点云数据进行归一化
    :param pc: 需要归一化的点云数据
    :return: 归一化后的点云数据
    """
    # 求质心，也就是一个平移量，实际上就是求均值
    centroid = np.mean(pc, axis=0)
    # 置于原点
    pc = pc - centroid
    # 求最长轴
    m = np.max(np.sqrt(np.sum(pc ** 2, axis=1)))
    # 对点云进行缩放（-1 1）
    pc = pc / m

    # 反归一化
    # ret = pred * m + centroid
    return pc
```