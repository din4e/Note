# 代码库

方便复制粘贴。

## 处理CSV或类CSV的输入方式

```cpp
void input(std::string filename)
{
	std::ifstream in(filename);
	std::string line;
	size_t sizeV, sizeE;
	std::getline(in, line, ','), sizeV = atoi(line.c_str());
	std::getline(in, line), sizeE = atoi(line.c_str());
	this->clear();
	this->v.resize(sizeV);
	this->e.resize(sizeE);
	for (size_t i = 0; i < sizeE; i++) {
		std::getline(in, line, ','), this->e[i].h = atoi(line.c_str());
		std::getline(in, line), this->e[i].e = atoi(line.c_str());
		v[this->e[i].h].neighbours.emplace_back(this->e[i].e), v[this->e[i].e].neighbours.emplace_back(this->e[i].h);
	}
	size_t i = 0;
	std::for_each(this->v.begin(), this->v.end(), [&i](vertex &v) {v.id = i++; });
	this->getName();

	if (printVertexWhileInput) printV();
}
```

```cpp
void SplitString(const std::string& s, std::vector<std::string>& v, const std::string& c){
	std::string::size_type pos1, pos2;
	pos2 = s.find(c);pos1 = 0;
	while(std::string::npos != pos2){
		v.push_back(s.substr(pos1, pos2-pos1));
    	pos1 = pos2 + c.size();pos2 = s.find(c, pos1);
  	}
  	if(pos1 != s.length()) v.push_back(s.substr(pos1));
}
```

## vector 和数组转换

```cpp
int a[]={0,0,1,1};
vector<int> varr(arr, arr+5);
//OR
std::vector<int> v({0,0,1,1});
```