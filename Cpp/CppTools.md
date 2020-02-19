# 代码库

方便复制粘贴。

## 1. `String`类

### [单个`char`转`string`](https://blog.csdn.net/carbon06/article/details/79353821)
```cpp
const char c = 'a';

// 1. 使用 string 的构造函数
string s(1,c);

// 2. 声明string 后将char push_back
string s1;
s1.push_back(c);

// 3.使用stringstream
stringstream ss;
ss << c;
string str2 = ss.str();

cout << to_string(c) << endl;
```

## 2. 输入输出处理

### 处理`CSV`文件或类`CSV`的输入方式

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
	pos2 = s.find(c);pos1 = 0;v.clear();
	while(std::string::npos != pos2){
		v.push_back(s.substr(pos1, pos2-pos1));
    	pos1 = pos2 + c.size();pos2 = s.find(c, pos1);
  	}
  	if(pos1 != s.length()) v.push_back(s.substr(pos1));
}
```

## 3. `STL`注意事项以及技巧

### `vector`和数组转换

```cpp
int a[]={0,0,1,1};
vector<int> varr(arr, arr+5);
//OR
std::vector<int> v({0,0,1,1});
```

## 4. 有趣的基础知识

### 4.1 `for`循环
 
#### 4.1.1 用字符串做循环内容

```cpp
for (char i = 'a'; i < 'y'; i++) {
	string filename(1,i); 
	filename= "data/enum/" + filename + ".csv";
}
```
#### 4.1.2 定义双变量

```cpp
for(i=0,j=s.size()-1;i<j;i++,j--) swap(s[i],s[j]);
```

#### 5. `ZTIME`
```cpp
#include<ctime>
class ztime
{
public:
	ztime() { this->b_ = this->p_ = clock(); };
	void begin() {
		this->b_ = this->p_ = clock(); 
	};
	void end() {
		this->e_ = clock(); 
		this->t = (double(this->e_) - double(this->b_)) / CLOCKS_PER_SEC;
	}
	double data() {
		this->e_ = clock(); 
		this->p_ = this->e_;
		this->t = (double(this->e_) - double(this->b_)) / CLOCKS_PER_SEC;
		return this->t;
	};
	double pre() { 
		this->e_ = clock();
		this->t = (double(this->e_) - double(this->p_)) / CLOCKS_PER_SEC;
		this->p_ = this->e_;
		return this->t;
	};
private:
	clock_t    b_ = 0, p_ = 0, e_ = 0;
	double     t = 0;
};
#define ZTIME ztime time;
```

## 6. RNG randi() randf()
```cpp
//RNG...
#define NN 624
#define MM 397
#define MATRIX_A 0x9908b0df   /* constant vector a */
#define UPPER_MASK 0x80000000 /* most significant w-r bits */
#define LOWER_MASK 0x7fffffff /* least significant r bits */
#define TEMPERING_MASK_B 0x9d2c5680
#define TEMPERING_MASK_C 0xefc60000
#define TEMPERING_SHIFT_U(y)  (y >> 11)
#define TEMPERING_SHIFT_S(y)  (y << 7)
#define TEMPERING_SHIFT_T(y)  (y << 15)
#define TEMPERING_SHIFT_L(y)  (y >> 18)

static unsigned long mt[NN];  /* the array for the state vector  */
static int mti = NN + 1;      /* mti==NN+1 means mt[NN] is not initialized */
void sgenrand(unsigned long seed)
{
	int i;
	for (i = 0; i < NN; i++)
	{
		mt[i] = seed & 0xffff0000;
		seed = 69069 * seed + 1;
		mt[i] |= (seed & 0xffff0000) >> 16;
		seed = 69069 * seed + 1;
	}
	mti = NN;
}
void lsgenrand(unsigned long seed_array[])
{
	int i;
	for (i = 0; i < NN; i++)
		mt[i] = seed_array[i];
	mti = NN;
}
double genrand()
{
	unsigned long y;
	static unsigned long mag01[2] = { 0x0, MATRIX_A };
	if (mti >= NN)
	{
		int kk;
		if (mti == NN + 1) sgenrand(4357);
		for (kk = 0; kk < NN - MM; kk++) {
			y = (mt[kk] & UPPER_MASK) | (mt[kk + 1] & LOWER_MASK);
			mt[kk] = mt[kk + MM] ^ (y >> 1) ^ mag01[y & 0x1];
		}
		for (; kk < NN - 1; kk++) {
			y = (mt[kk] & UPPER_MASK) | (mt[kk + 1] & LOWER_MASK);
			mt[kk] = mt[kk + (MM - NN)] ^ (y >> 1) ^ mag01[y & 0x1];
		}
		y = (mt[NN - 1] & UPPER_MASK) | (mt[0] & LOWER_MASK);
		mt[NN - 1] = mt[MM - 1] ^ (y >> 1) ^ mag01[y & 0x1];
		mti = 0;
	}
	y = mt[mti++]; y ^= TEMPERING_SHIFT_U(y); y ^= TEMPERING_SHIFT_S(y) & TEMPERING_MASK_B;
	y ^= TEMPERING_SHIFT_T(y) & TEMPERING_MASK_C; y ^= TEMPERING_SHIFT_L(y);
	return y;
}

double randf() { return ((double)genrand() * 2.3283064370807974e-10); }
long   randi(unsigned long LIM) { return((unsigned long)genrand() % LIM); }
```